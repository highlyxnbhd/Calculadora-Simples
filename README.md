import tkinter as tk
from tkinter import messagebox
import math

class ScientificCalculator(tk.TK):
    def __init__(self):
        super().__init__()
        self.title("Calculadora Cientifica")
        self.geometry("400x600")
        self.resizable(False, False)
        self.init_ui()

    def unit_ui(self):
        self.entry = tk.Entry(self, front=("Arial", 20), borderwidth=2, relief="solid")
        self.entry.grid(row=0, column=0, columnsplan=5, pady=10, padx=10)

        butoons = [
            '7', '8', '9', '/', 'sqrt',
            '4', '5', '6', '*', 'log',
            '1', '2', '3', '-', 'sin',
            '0', '.', '=', '+', 'cos',
            '(', ')', '^', 'tan', 'pi',
            'C'
        ]

        row_val = 1
        col_val = 0

        for button in butoons:
            action = lambda x=button: self.on_button_click(x)
            tk.Button(self, text=button, width=5, height=2, font=("Arial", 18),command=action).grid(row=row_val, colimn=col_val)
            col_val+= 1
            if col_val > 4:
                col_val = 0
                row_val += 1

def on_button_click(self, button):
    if button == 'C':
        self.entry.delete(0, tk.END)
    elif button =='=':
        try:
            expression = self.entry.get()
            expression = expression.replace('sqrt', 'math.sqrt')
            expression = expression.replace('sin', 'math.sin')
            expression = expression.replace('cos', 'math.cos')
            expression = expression.replace('tan', 'math.tan')
            expression = expression.replace('log', 'math.log')
            expression = expression.replace('pi', str(math.pi))
            expression = expression.replace('^', '**')
            result = eval(expression)
            self.entry.delete(0, tk.END)
            self.entry.insert(tk.END, str(result))
        except Exception as e:
            messagebox.showerror("Erro", "Entrada Inválida")
    else:
        self.entry.insert(tk.END, button)

if __name__ == "__main__":
    app= ScientificCalculator()
    app.mainloop()
