# database-using-mongodb
import pymongo

# Connect to MongoDB
client = pymongo.MongoClient("mongodb://localhost:27017/")
database = client["library_database"]

# Define collections
books_collection = database["books"]
authors_collection = database["authors"]

def print_books():
    print("Books in the library:")
    for book in books_collection.find():
        print(book)

def add_book():
    print("Adding a new book:")
    title = input("Enter the title: ")
    author_id = int(input("Enter the author's ID: "))
    publication_year = int(input("Enter the publication year: "))

    new_book = {"title": title, "author_id": author_id, "publication_year": publication_year}
    books_collection.insert_one(new_book)
    print("Book added successfully!")

def update_book():
    print("Updating a book:")
    book_id = int(input("Enter the book's ID to update: "))
    new_title = input("Enter the new title: ")

    books_collection.update_one({"book_id": book_id}, {"$set": {"title": new_title}})
    print("Book updated successfully!")

def delete_book():
    print("Deleting a book:")
    book_id = int(input("Enter the book's ID to delete: "))

    books_collection.delete_one({"book_id": book_id})
    print("Book deleted successfully!")

# Interactive menu
while True:
    print("\nLibrary Management System")
    print("1. Print all books")
    print("2. Add a new book")
    print("3. Update a book")
    print("4. Delete a book")
    print("5. Exit")

    choice = input("Enter your choice (1-5): ")

    if choice == "1":
        print_books()
    elif choice == "2":
        add_book()
    elif choice == "3":
        update_book()
    elif choice == "4":
        delete_book()
    elif choice == "5":
        print("Exiting the program. Goodbye!")
        break
    else:
        print("Invalid choice. Please enter a number between 1 and 5.")
