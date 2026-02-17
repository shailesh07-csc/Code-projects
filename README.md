from database import Database
from auth import Auth
import getpass

def user_menu(db, user_id):
    while True:
        print("\n==== Expense Tracker ====")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Category Summary")
        print("4. Logout")

        choice = input("Enter choice: ")

        if choice == "1":
            amount = float(input("Amount: "))
            category = input("Category: ")
            description = input("Description: ")
            db.add_expense(user_id, amount, category, description)
            print("✅ Expense Added!")

        elif choice == "2":
            expenses = db.get_expenses(user_id)
            print("\n--- Your Expenses ---")
            for exp in expenses:
                print(f"{exp[0]} | ₹{exp[1]} | {exp[2]} | {exp[3]}")

        elif choice == "3":
            summary = db.category_summary(user_id)
            print("\n--- Category Summary ---")
            for item in summary:
                print(f"{item[0]}: ₹{item[1]}")

        elif choice == "4":
            break

        else:
            print("Invalid choice.")


def main():
    db = Database()
    auth = Auth(db)

    while True:
        print("\n==== Welcome ====")
        print("1. Register")
        print("2. Login")
        print("3. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            username = input("Username: ")
            password = getpass.getpass("Password: ")
            auth.register(username, password)

        elif choice == "2":
            username = input("Username: ")
            password = getpass.getpass("Password: ")
            user_id = auth.login(username, password)

            if user_id:
                print("✅ Login Successful!")
                user_menu(db, user_id)
            else:
                print("❌ Invalid Credentials!")

        elif choice == "3":
            break

        else:
            print("Invalid choice.")


if __name__ == "__main__":
    main()# Code-projects
Code project description 
