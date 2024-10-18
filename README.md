# Calculator

A simple calculator built using Python's `tkinter` library. This calculator supports basic arithmetic operations and has a simple user interface with different colors for numbers and operators.

## Features

- Supports addition, subtraction, multiplication, and division.
- Clear (`C`) button to reset the input.
- Equals (`=`) button to calculate the result.
- Grey color for number buttons, and orange color for operator buttons.
- Responsive and user-friendly interface with rounded buttons.

## Prerequisites

- Python 3.x
- Tkinter (usually included with Python)

## How to Run

1. Clone the repository:
    ```bash
    git clone https://github.com/aditya91203/Calculator.git
    ```
2. Navigate to the directory:
    ```bash
    cd Calculator
    ```
3. Run the calculator script:
    ```bash
    python Calculator.py
    ```

## Code

Here's the main code for the calculator:

```python
import tkinter as tk

# Function to evaluate the expression
def evaluate_expression(expression):
    try:
        result = eval(expression)
        entry_var.set(result)
    except Exception as e:
        entry_var.set("Error")

# Function to update the entry field
def update_entry(value):
    current_text = entry_var.get()
    entry_var.set(current_text + str(value))

# Function to clear the entry field
def clear_entry():
    entry_var.set("")

# Create the main window
root = tk.Tk()
root.title("Calculator")

# Create a StringVar to hold the entry text
entry_var = tk.StringVar()

# Create the entry widget
entry = tk.Entry(root, textvariable=entry_var, font=('Arial', 24), bd=10, insertwidth=2, width=14, borderwidth=4)
entry.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

# Define button colors and style
number_button_color = "#A9A9A9"  # Grey for numbers
operator_button_color = "#FF8C00"  # Orange for operators
button_radius = 50  # Round appearance
button_font = ('Arial', 18)

# Create buttons for digits and operations
buttons = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    '0', 'C', '=', '+'
]

# Function to apply the style and color to the buttons
def create_button(text, row, col, color, action):
    tk.Button(root, text=text, padx=20, pady=20, font=button_font, bg=color, fg="white", bd=5, relief="ridge", command=action).grid(row=row, column=col, padx=5, pady=5)

# Create and place buttons in the grid
row_val = 1
col_val = 0
for button in buttons:
    if button == '=':
        action = lambda: evaluate_expression(entry_var.get())
        create_button(button, row_val, col_val, operator_button_color, action)
    elif button == 'C':
        action = clear_entry
        create_button(button, row_val, col_val, operator_button_color, action)
    elif button in ['/', '*', '-', '+']:
        action = lambda x=button: update_entry(x)
        create_button(button, row_val, col_val, operator_button_color, action)
    else:
        action = lambda x=button: update_entry(x)
        create_button(button, row_val, col_val, number_button_color, action)
    
    col_val += 1
    if col_val > 3:
        col_val = 0
        row_val += 1

# Run the application
root.mainloop()

![calci](https://github.com/user-attachments/assets/6d87e4ac-b152-4956-83f7-b5610f2418ec)
