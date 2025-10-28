import tkinter as tk

def btn_click(item):
    global expression
    expression += str(item)
    input_text.set(expression)

def btn_clear():
    global expression
    expression = ""
    input_text.set("")

def btn_equal():
    global expression
    try:
        result = str(eval(expression))
        input_text.set(result)
        expression = ""
    except:
        input_text.set("Error")
        expression = ""

window = tk.Tk()
window.title("Simple Calculator")
window.geometry("400x500")

expression = ""
input_text = tk.StringVar()

input_frame = tk.Frame(window)
input_frame.pack()

input_field = tk.Entry(input_frame, textvariable=input_text, font=('Times New Romand', 18, 'bold'), bd=10, insertwidth=2, width=14, justify='right')
input_field.grid(row=0, column=0)
input_field.pack(ipady=10)

btns_frame = tk.Frame(window)
btns_frame.pack()

buttons = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    'C', '0', '=', '+'
]

row, col = 0, 0
for button in buttons:
    action = lambda x=button: btn_click(x) if x not in ['C', '='] else (btn_clear() if x == 'C' else btn_equal())
    tk.Button(btns_frame, text=button, width=10, height=3, command=action).grid(row=row, column=col)
    col += 1
    if col == 4:
        col = 0
        row += 1

window.mainloop()

