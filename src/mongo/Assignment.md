# Assignment 3 - Mongo

## Part 1 (10 pts): Day 1 - Reading

1. Read Day 1 and work through the examples. Dump your database into a
    directory named data.

## Part 2 (10 pts): Day 1 - Find

Complete the "Find" homework in Day 1.

1. Bookmark the online MongoDB documentation and read up on something
    you found intriguing today. Provide the URL.

https://www.mongodb.com/docs/manual/aggregation/


2. Look up how to construct regular expressions in Mongo. Provide the URL.

https://www.mongodb.com/docs/manual/reference/operator/query/regex/


3. Acquaint yourself with command-line db.help() and db.collections.help() output.
    Nothing to provide.



4. Find a Mongo driver in your programming language of choice (Ruby, Java,
    PHP, Go, Elixir, and so on). Provide URL to list of drivers/libraries for
    different languages.
https://www.mongodb.com/docs/drivers/


## Part 3 (15 pts): Create and populate a database to hold library books and patrons.
For each of the steps below, provide the mongodb code that accomplishes this. Store your work in a folder called “Library”.

### Step 1: Create the Database

For this assignment, you will be working with the two collections described below. **Use the exact document and attribute names provided!**
* books - stores information about library books
    * Should use attributes of:  title, author, isbn, genre, publishedYear, copiesAvailable, and totalCopies
    * Make sure that some of your books are in the “Fiction” genre and some are in “Non-Fiction”
    * Make sure that at least two of your books have copies available to check out.
* patrons - stores information about library members
    * Should use attributes of:    name, email, membershipDate, booksCheckedOut (array of title and dueDate), and fines.
    * Make sure that at least one of your patrons has checked out more than one book.
    * Make sure that at least one of your patrons has an overdue fine.
    * Make sure that at least one of your patrons joined the library in 2004.

### Step 2: Insert Books into the Library
Insert six of your favorite books into the library.  Make sure that these are your favorite books, not randomly generated books.
db.books.insertMany([
  { title:"The Silent Patient", author:"Alex Michaelides", isbn:"9781250301697",
    genre:"Fiction", publishedYear:2019, copiesAvailable:3, totalCopies:5 },
  { title:"Educated", author:"Tara Westover", isbn:"9780399590504",
    genre:"Non-Fiction", publishedYear:2018, copiesAvailable:0, totalCopies:4 },
  { title:"Clean Code", author:"Robert C. Martin", isbn:"9780132350884",
    genre:"Non-Fiction", publishedYear:2008, copiesAvailable:2, totalCopies:2 },
  { title:"Project Hail Mary", author:"Andy Weir", isbn:"9780593135204",
    genre:"Fiction", publishedYear:2021, copiesAvailable:1, totalCopies:6 },
  { title:"Thinking, Fast and Slow", author:"Daniel Kahneman", isbn:"9780374533557",
    genre:"Non-Fiction", publishedYear:2011, copiesAvailable:0, totalCopies:3 },
  { title:"The Night Circus", author:"Erin Morgenstern", isbn:"9780307744432",
    genre:"Fiction", publishedYear:2011, copiesAvailable:4, totalCopies:7 },
]);

### Step 3: Insert Patrons into the Library
Insert five of your friends as patrons into the library. Make sure that these are not randomly generated.

db.patrons.insertMany([
  { name:"Divya Prathipati", email:"divya@example.edu",
    membershipDate: ISODate("2004-06-15T00:00:00Z"),
    booksCheckedOut:[
      { title:"The Silent Patient", dueDate: ISODate("2025-10-28T00:00:00Z") },
      { title:"Clean Code",        dueDate: ISODate("2025-11-04T00:00:00Z") }
    ],
    fines:0
  },
  { name:"Rani Prathipati", email:"rani@example.com",
    membershipDate: ISODate("2016-03-02T00:00:00Z"),
    booksCheckedOut:[ { title:"Educated", dueDate: ISODate("2025-10-25T00:00:00Z") } ],
    fines:7.50
  },
  { name:"Rambabu Prathipati", email:"rambabu@example.com",
    membershipDate: ISODate("2020-09-01T00:00:00Z"),
    booksCheckedOut:[], fines:0
  }
]);

### Step 4: Queries
For each of the queries below, write the query and include the results.

1. Write a query to find the titles of all books that have at least one copy available for checkout.

db.books.find(
...   { copiesAvailable: { $gte: 1 } },
...   { _id: 0, title: 1 }
... )
{ "title" : "The Silent Patient" }
{ "title" : "Clean Code" }
{ "title" : "Project Hail Mary" }
{ "title" : "The Night Circus" }
>

2. Write a query to find the authors of all books in the "Fiction" genre.

> db.books.distinct("author", { genre: "Fiction" })
[ "Alex Michaelides", "Andy Weir", "Erin Morgenstern" ]
>

3. Write a query to find the names of all patrons who owe fines (fines greater than $0).

> db.patrons.find(
...   { fines: { $gt: 0 } },
...   { _id: 0, name: 1 }
... )
{ "name" : "Rani Prathipati" }
>

4. Write a query to find the names and membership date of all patrons who became members in the year 2024.

> db.patrons.find(
...   {
...     membershipDate: {
...       $gte: ISODate("2024-01-01T00:00:00Z"),
...       $lt:  ISODate("2025-01-01T00:00:00Z")
...     }
...   },
...   { _id: 0, name: 1, membershipDate: 1 }
... )
>

Hint: Use $gte and $lt operators to specify a date range from January 1, 2024 to January 1, 2025.

## Part 4 (10 pts): Day 2 - Do

Complete the "Find" homework in Day 2.

1. Find a shortcut for admin commands. Write the shortcut here.


2. Find the online documentation for queries and cursors. Write the URL here.


3. Find the MongoDB documentation for mapreduce. Write the URL here.


4. Through the JavaScript interface, investigate the code for three collections
    functions: help(), findOne(), and stats(). Past the code for each below.
    For each, write a one-sentence insight that you learned by looking at
    the code.
