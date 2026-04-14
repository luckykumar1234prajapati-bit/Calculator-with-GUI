import tkinter as tk


def press(num):
    global expression
    expression += str(num)
    equation.set(expression)

def equalpress():
    global expression
    try:
        total = str(eval(expression))
        equation.set(total)
        expression = total
    except:
        equation.set("Error")
        expression = ""

def clear():
    global expression
    expression = ""
    equation.set("")

root = tk.Tk()
root.title("Calculator")
root.geometry("300x400")
root.resizable(False, False)

expression = ""
equation = tk.StringVar()

entry = tk.Entry(root, textvariable=equation, font=("Arial", 20), bd=10, relief=tk.RIDGE, justify='right')
entry.pack(fill=tk.BOTH, ipadx=8, pady=10, padx=10)

# Buttons frame
frame = tk.Frame(root)
frame.pack()

buttons = [
    ['7', '8', '9', '/'],
    ['4', '5', '6', '*'],
    ['1', '2', '3', '-'],
    ['0', '.', '=', '+']
]

for row in buttons:
    row_frame = tk.Frame(frame)
    row_frame.pack(expand=True, fill="both")

    for btn in row:
        if btn == "=":
            action = equalpress
        else:
            action = lambda x=btn: press(x)

        tk.Button(
            row_frame,
            text=btn,
            font=("Arial", 15),
            height=2,
            width=5,
            command=action
        ).pack(side="left", expand=True, fill="both")

tk.Button(
    root,
    text="C",
    font=("Arial", 15),
    height=2,
    command=clear
).pack(fill="both", padx=10, pady=5)

root.mainloop()
