# SQLite3 in Python :

- SQL is a standard language for managing and manipulating relational databases. SQLite is a self-contained, serverless and zero-configuration database engine that is widely used for embedded database systems.  

```py
import sqlite3

## Connect to a sqlite databse
connection = sqlite3.connect('example.db')

cursor = connection.cursor()

## Creating a Table
cursor.execute('''
CREATE TABLE IF NOT EXISTS employees(
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER,
    department TEXT
)
''')

## Commit the changes :
connection.commit()

cursor.execute('''
    SELECT * FROM employees
''')

## Insert data in sqlite table :
cursor.execute('''
    INSERT INTO employees(name, age, department)
    VALUES ('Bob', 25, 'Comp')
''')
cursor.execute('''
    INSERT INTO employees(name, age, department)
    VALUES ('Charlie', 35, 'Comp')
''')
cursor.execute('''
    INSERT INTO employees(name, age, department)
    VALUES ('Jack', 15, 'Comp')
''')

connection.commit()

## Insert Multiple values in  one execution :

sales_data = [
    ('Bob', 34, 'sales'),
    ('JAck', 21, 'HR'),
    ('Job', 10, 'sales'),
    ('Nine', 50, 'HR')
    
]
cursor.executemany('''
   INSERT INTO employees (name, age, department)
   Values(?,?,?,?) 
''', sales_data)
```

#### Access the data from sqlite Tables :

```py
cursor.execute('SELECT * FROM employees')
rows = cursor.fetchall()

for row in rows :
    print(row) # Tuples get printed
```

#### Update data in sqlite table :

```py
cursor.execute('''
    UPDATE employees
        SET age = 34
        WHERE name = 'Bob'
''')

connection.commit()
```

#### Delete data in sqlite table :

```py
cursor.execute('''
    DELETE FROM employees
    WHERE name = 'Bob'
''')

connection.commit()
```

#### Permanently close the connection :

```py
connection.close()
```