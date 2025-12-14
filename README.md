import os

# File to store income and expense records
RECORDS_FILE = "daily_records.txt"

# Function to load records from the file
def load_records():
    if not os.path.exists(RECORDS_FILE):
        return []
    
    with open(RECORDS_FILE, "r") as file:
        records = file.readlines()
    
    return [record.strip() for record in records]

# Function to save records to the file
def save_records(records):
    with open(RECORDS_FILE, "w") as file:
        for record in records:
            file.write(record + "\n")

# Function to add an income record
def add_income(amount, description):
    records = load_records()
    record = f"Income: {amount} - {description}"
    records.append(record)
    save_records(records)
    print(f"Income added: {amount} - {description}")

# Function to add an expense record
def add_expense(amount, description):
    records = load_records()
    record = f"Expense: {amount} - {description}"
    records.append(record)
    save_records(records)
    print(f"Expense added: {amount} - {description}")

# Function to view all records and calculate totals
def view_records():
    records = load_records()
    if records:
        total_income = 0
        total_expense = 0
        print("\nDaily Income and Expense Records:")
        for record in records:
            print(record)
            # Calculate totals
            if "Income" in record:
                total_income += float(record.split(":")[1].split(" - ")[0].strip())
            elif "Expense" in record:
                total_expense += float(record.split(":")[1].split(" - ")[0].strip())
        
        balance = total_income - total_expense
        print(f"\nTotal Income: {total_income}")
        print(f"Total Expenses: {total_expense}")
        print(f"Balance: {balance}")
    else:
        print("No records found.")

# Main menu
def main():
    while True:
        print("\nIncome and Expense Tracker")
        print("1. View Records")
        print("2. Add Income")
        print("3. Add Expense")
        print("4. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            view_records()
        elif choice == "2":
            amount = float(input("Enter the amount of income: "))
            description = input("Enter a description for the income: ")
            add_income(amount, description)
        elif choice == "3":
            amount = float(input("Enter the amount of expense: "))
            description = input("Enter a description for the expense: ")
            add_expense(amount, description)
        elif choice == "4":
            print("Exiting the Income and Expense Tracker.")
            break
        else:
            print("Invalid choice, please try again.")

# Run the program
if __name__ == "__main__":
    main()
