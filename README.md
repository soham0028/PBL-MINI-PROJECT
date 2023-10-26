# PBL-MINI-PROJECT

import tkinter as tk
from tkinter import messagebox

class ExpenseTracker:
    def __init__(self, root):
        self.root = root
        self.root.title("Expense Tracker")

        # Initialize variables
        self.expenses = []
        self.total_expense = 0
        self.salary = 0

        # Create GUI elements
        self.expense_label = tk.Label(root, text="Enter Expense:")
        self.expense_entry = tk.Entry(root)
        self.expense_category_label = tk.Label(root, text="Expense Category:")
        self.expense_category_entry = tk.Entry(root)
        self.comment_label = tk.Label(root, text="Comments:")
        self.comment_entry = tk.Entry(root)
        self.add_button = tk.Button(root, text="Add Expense", command=self.add_expense)
        self.salary_label = tk.Label(root, text="Your Salary:")
        self.salary_entry = tk.Entry(root)
        self.calculate_button = tk.Button(root, text="Calculate Total", command=self.calculate_total)
        self.total_label = tk.Label(root, text="Total Expenses: $0")

        # Create a listbox to display expenses
        self.expense_listbox = tk.Listbox(root)
        self.expense_listbox.pack()

        # Layout GUI elements
        self.expense_label.pack()
        self.expense_entry.pack()
        self.expense_category_label.pack()
        self.expense_category_entry.pack()
        self.comment_label.pack()
        self.comment_entry.pack()
        self.add_button.pack()
        self.salary_label.pack()
        self.salary_entry.pack()
        self.calculate_button.pack()
        self.total_label.pack()

    def add_expense(self):
        expense = self.expense_entry.get()
        category = self.expense_category_entry.get()
        comment = self.comment_entry.get()
        if expense and category:
            expense_data = {"expense": float(expense), "category": category, "comment": comment}
            self.expenses.append(expense_data)
            formatted_expense = "${:.2f} ({}) : {}".format(float(expense), category, comment)
            self.expense_listbox.insert(tk.END, formatted_expense)
            self.expense_entry.delete(0, 'end')
            self.expense_category_entry.delete(0, 'end')
            self.comment_entry.delete(0, 'end')
        else:
            messagebox.showerror("Error", "Please enter both expense and category.")

    def calculate_total(self):
        salary = self.salary_entry.get()
        if salary:
            self.salary = float(salary)
            self.total_expense = sum(expense['expense'] for expense in self.expenses)
            self.total_label.config(text=f"Total Expenses: ${self.total_expense:.2f} (Remaining: ${self.salary - self.total_expense:.2f})")
        else:
            messagebox.showerror("Error", "Please enter your salary.")

if __name__ == "__main__":
    root = tk.Tk()
    app = ExpenseTracker(root)
    root.mainloop()
