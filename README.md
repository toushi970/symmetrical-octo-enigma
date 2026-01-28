class Book:
    def __init__(self, title, author, genre):
        self.title = title
        self.author = author
        self.genre = genre
        self.is_available = True

    def borrow_book(self):
        if self.is_available:
            self.is_available = False
            print(f"You have borrowed '{self.title}'.")
        else:
            print(f"Sorry, '{self.title}' is currently not available.")

    def return_book(self):
        if not self.is_available:
            self.is_available = True
            print(f"You have returned '{self.title}'.")
        else:
            print(f"'{self.title}' was not borrowed.")

    def __str__(self):
        availability = 'Available' if self.is_available else 'Checked Out'
        return f"Title: {self.title}, Author: {self.author[0]}, Genre: {self.genre}, Status: {availability}"


class Library:
    def __init__(self):
        self.books = []
        self.genres = set()
        self.authors_books = {}

    def add_book(self, book):
        self.books.append(book)
        self.genres.add(book.genre)
        author_name = book.author[0]
        if author_name in self.authors_books:
            self.authors_books[author_name].append(book)
        else:
            self.authors_books[author_name] = [book]
        print(f"Book '{book.title}' added to the library.")

    def remove_book(self, book_title):
        book_to_remove = None
        for book in self.books:
            if book.title.lower() == book_title.lower():
                book_to_remove = book
                break
        if book_to_remove:
            self.books.remove(book_to_remove)
            author_name = book_to_remove.author[0]
            self.authors_books[author_name].remove(book_to_remove)
            if not self.authors_books[author_name]:
                del self.authors_books[author_name]
            genre_books = [b for b in self.books if b.genre == book_to_remove.genre]
            if not genre_books:
                self.genres.remove(book_to_remove.genre)
            print(f"Book '{book_to_remove.title}' removed from the library.")
        else:
            print(f"Book '{book_title}' not found in the library.")

    def find_books_by_author(self, author_name):
        return self.authors_books.get(author_name, [])

    def find_books_by_genre(self, genre):
        return [book for book in self.books if book.genre.lower() == genre.lower()]

    def show_all_books(self):
        if not self.books:
            print("No books in the library.")
        else:
            for book in self.books:
                print(book)

    def get_book_by_title(self, book_title):
        for book in self.books:
            if book.title.lower() == book_title.lower():
                return book
        return None


class User:
    def __init__(self, name):
        self.name = name
        self.borrowed_books = set()

    def borrow_book(self, library, book_title):
        book = library.get_book_by_title(book_title)
        if book:
            if book.is_available:
                book.borrow_book()
                self.borrowed_books.add(book.title)
            else:
                print(f"Sorry, '{book.title}' is currently not available.")
        else:
            print(f"Book '{book_title}' not found in the library.")

    def return_book(self, library, book_title):
        if book_title in self.borrowed_books:
            book = library.get_book_by_title(book_title)
            if book:
                book.return_book()
                self.borrowed_books.remove(book_title)
            else:
                print(f"Book '{book_title}' not found in the library.")
        else:
            print(f"You did not borrow '{book_title}'.")

    def __str__(self):
        return f"User: {self.name}, Borrowed Books: {', '.join(self.borrowed_books) if self.borrowed_books else 'None'}"


def display_menu():
    print("\n===== Library Management System =====")
    print("1. Add a Book")
    print("2. Remove a Book")
    print("3. Find Books by Author")
    print("4. Find Books by Genre")
    print("5. Show All Books")
    print("6. Borrow a Book")
    print("7. Return a Book")
    print("8. Show User Information")
    print("9. Exit")
    print("======================================")


def get_author_details():
    author_name = input("Enter author's name: ").strip()
    while True:
        try:
            year_of_birth = int(input("Enter author's year of birth: ").strip())
            break
        except ValueError:
            print("Please enter a valid year.")
    return (author_name, year_of_birth)


def main():
    library = Library()
    user = User("MJ Marky") 
    initial_books = [
        Book("Mere Christianity", ("C.S. Lewis", 1898), "Christian Apologetics"),
        Book("The Confessions of Saint Augustine", ("Saint Augustine", 354), "Christian Theology"),
        Book("The Pilgrim's Progress", ("John Bunyan", 1628), "Christian Allegory"),
        Book("The Cost of Discipleship"class Book:
    def __init__(self, title, author, genre):
        self.title = title
        self.author = author
        self.genre = genre
        self.is_available = True

    def borrow_book(self):
        if self.is_available:
            self.is_available = False
            print(f"You have borrowed '{self.title}'.")
        else:
            print(f"Sorry, '{self.title}' is currently not available.")

    def return_book(self):
        if not self.is_available:
            self.is_available = True
            print(f"You have returned '{self.title}'.")
        else:
            print(f"'{self.title}' was not borrowed.")

    def __str__(self):
        availability = 'Available' if self.is_available else 'Checked Out'
        return f"Title: {self.title}, Author: {self.author[0]}, Genre: {self.genre}, Status: {availability}"


class Library:
    def __init__(self):
        self.books = []
        self.genres = set()
        self.authors_books = {}

    def add_book(self, book):
        self.books.append(book)
        self.genres.add(book.genre)
        author_name = book.author[0]
        if author_name in self.authors_books:
            self.authors_books[author_name].append(book)
        else:
            self.authors_books[author_name] = [book]
        print(f"Book '{book.title}' added to the library.")

    def remove_book(self, book_title):
        book_to_remove = None
        for book in self.books:
            if book.title.lower() == book_title.lower():
                book_to_remove = book
                break
        if book_to_remove:
            self.books.remove(book_to_remove)
            author_name = book_to_remove.author[0]
            self.authors_books[author_name].remove(book_to_remove)
            if not self.authors_books[author_name]:
                del self.authors_books[author_name]
            genre_books = [b for b in self.books if b.genre == book_to_remove.genre]
            if not genre_books:
                self.genres.remove(book_to_remove.genre)
            print(f"Book '{book_to_remove.title}' removed from the library.")
        else:
            print(f"Book '{book_title}' not found in the library.")

    def find_books_by_author(self, author_name):
        return self.authors_books.get(author_name, [])

    def find_books_by_genre(self, genre):
        return [book for book in self.books if book.genre.lower() == genre.lower()]

    def show_all_books(self):
        if not self.books:
            print("No books in the library.")
        else:
            for book in self.books:
                print(book)

    def get_book_by_title(self, book_title):
        for book in self.books:
            if book.title.lower() == book_title.lower():
                return book
        return None


class User:
    def __init__(self, name):
        self.name = name
        self.borrowed_books = set()

    def borrow_book(self, library, book_title):
        book = library.get_book_by_title(book_title)
        if book:
            if book.is_available:
                book.borrow_book()
                self.borrowed_books.add(book.title)
            else:
                print(f"Sorry, '{book.title}' is currently not available.")
        else:
            print(f"Book '{book_title}' not found in the library.")

    def return_book(self, library, book_title):
        if book_title in self.borrowed_books:
            book = library.get_book_by_title(book_title)
            if book:
                book.return_book()
                self.borrowed_books.remove(book_title)
            else:
                print(f"Book '{book_title}' not found in the library.")
        else:
            print(f"You did not borrow '{book_title}'.")

    def __str__(self):
        return f"User: {self.name}, Borrowed Books: {', '.join(self.borrowed_books) if self.borrowed_books else 'None'}"


def display_menu():
    print("\n===== Library Management System =====")
    print("1. Add a Book")
    print("2. Remove a Book")
    print("3. Find Books by Author")
    print("4. Find Books by Genre")
    print("5. Show All Books")
    print("6. Borrow a Book")
    print("7. Return a Book")
    print("8. Show User Information")
    print("9. Exit")
    print("======================================")


def get_author_details():
    author_name = input("Enter author's name: ").strip()
    while True:
        try:
            year_of_birth = int(input("Enter author's year of birth: ").strip())
            break
        except ValueError:
            print("Please enter a valid year.")
    return (author_name, year_of_birth)


def main():
    library = Library()
    user = User("MJ Marky") 
    initial_books = [
        Book("Mere Christianity", ("C.S. Lewis", 1898), "Christian Apologetics"),
        Book("The Confessions of Saint Augustine", ("Saint Augustine", 354), "Christian Theology"),
        Book("The Pilgrim's Progress", ("John Bunyan", 1628), "Christian Allegory"),
        Book("The Cost of Discipleship"
