import os
import json

def load_contacts(filename):
    if os.path.exists(filename):
        with open(filename, 'r') as f:
            contacts = json.load(f)
    else:
        contacts = {}
    return contacts

def save_contacts(filename, contacts):
    with open(filename, 'w') as f:
        json.dump(contacts, f, indent=4)

def add_contact(contacts):
    name = input("Enter contact name: ")
    phone = input("Enter contact phone number: ")
    email = input("Enter contact email address: ")

    contacts[name] = {
        'phone': phone,
        'email': email
    }
    print(f"Contact '{name}' added successfully!")

def search_contact(contacts):
    name = input("Enter contact name to search: ")
    if name in contacts:
        print(f"Name: {name}")
        print(f"Phone: {contacts[name]['phone']}")
        print(f"Email: {contacts[name]['email']}")
    else:
        print(f"Contact '{name}' not found.")

def display_contacts(contacts):
    if not contacts:
        print("No contacts found.")
    else:
        print("List of contacts:")
        for name, info in contacts.items():
            print(f"Name: {name}")
            print(f"Phone: {info['phone']}")
            print(f"Email: {info['email']}")
            print("")

def main():
    filename = "contacts.json"
    contacts = load_contacts(filename)

    while True:
        print("\n=== Contact Book Menu ===")
        print("1. Add a new contact")
        print("2. Search for a contact")
        print("3. Display all contacts")
        print("4. Quit")

        choice = input("Enter your choice (1-4): ")

        if choice == '1':
            add_contact(contacts)
        elif choice == '2':
            search_contact(contacts)
        elif choice == '3':
            display_contacts(contacts)
        elif choice == '4':
            save_contacts(filename, contacts)
            print("Contacts saved. Exiting program.")
            break
        else:
            print("Invalid choice. Please enter a number from 1 to 4.")

if __name__ == "__main__":
    main()

