# expense_tracker.py

import json

expenses = []

def add_expense():
    amount = input("Enter expense amount: ")
    category = input("Enter category: ")
    expenses.append({"amount": amount, "category": category})
    print("Expense added!")

def view_expenses():
    if not expenses:
        print("No expenses recorded.")
    else:
        for exp in expenses:
            print(f"{exp['amount']} - {exp['category']}")

def save_data():
    with open("expenses.json", "w") as f:
        json.dump(expenses, f)
    print("Data saved.")

def load_data():
    global expenses
    try:
        with open("expenses.json", "r") as f:
            expenses = json.load(f)
        print("Data loaded.")
    except FileNotFoundError:
        print("No data file found.")

def search_by_category():
    cat = input("Enter category to search: ")
    found = [e for e in expenses if e['category'].lower() == cat.lower()]
    for e in found:
        print(f"{e['amount']} - {e['category']}")

def menu():
    while True:
        print("\n1. Add Expense\n2. View Expenses\n3. Search by Category\n4. Save\n5. Load\n6. Exit")
        choice = input("Choose an option: ")
        if choice == "1":
            add_expense()
        elif choice == "2":
            view_expenses()
        elif choice == "3":
            search_by_category()
        elif choice == "4":
            save_data()
        elif choice == "5":
            load_data()
        elif choice == "6":
            break
        else:
            print("Invalid choice")

menu()


