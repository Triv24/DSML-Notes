##CRUD Operations with SQLite3 and Python


## `SQLite` :
-A lightweight version of SQL.
-It does not need a server and does not need setup.
-The database is stored directly as a file on your computer.

## `SQL` :
-A Structured Query language used to manage and work with databases.

## `Importing SQLite in Python` :
```py
import sqlite3
```

## `Create & Connect to Database` :
-This creates a new database file named example.db.
```py
connection = sqlite3.connect('example.db')

```
## `Create Cursor `:
-A cursor  is an obj that allows Python to execute SQL commands and work with the results.
- middleman between Python and the database.
```py
cursor = connection.cursor()
```

## `Create a Table (employees)`:
-cursor.execute() is used to run an SQL command in the database.
-commit() means save the changes permanently to the database.
-Without commit, the table creation would be temporary, and could be lost.


```py
cursor.execute('''
CREATE TABLE IF NOT EXISTS employees(
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER,
    department TEXT
)
''')
connection.commit()

```
## `Insert a data in Table (employees)`:
#1.inserting each data one by one 
```py
cursor.execute("INSERT INTO employees (name, age, department) VALUES ('Krish', 32, 'Data Scientist')")
cursor.execute("INSERT INTO employees (name, age, department) VALUES ('Bob', 25, 'Engineering')")
cursor.execute("INSERT INTO employees (name, age, department) VALUES ('Charlie', 35, 'Finance')")
connection.commit()
```
#2.Inserting bulk data :
```py
emp_data = [
    ('Bob', 30, 'IT'),
    ('Raj',15, 'HR'),
    ('siya',20, 'Marketing'),
    ('Riya', 25, 'HR')
]

cursor.executemany(
    'INSERT INTO employees (name ,age,department) VALUES (?, ?, ?)',
    emp_data
)
connection.commit()

```


## `Updating a Table (employees)`:

```py
cursor.execute("UPDATE employees SET age = 34 WHERE name = 'Krish'")
connection.commit()

```


## `Deleting data from  Table (employees)`:

```py
cursor.execute("DELETE FROM employees WHERE name = 'Bob'")
connection.commit()

```
## `Reading data from  Table (employees)`:
-collects all those records and stores them in rows
```py
cursor.execute("SELECT * FROM employees")
rows = cursor.fetchall()
for row in rows:
    print(row)

```
## Close Connection

```py
connection.close()

```