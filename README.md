MODULE 05 – PYTHON APPLICATION DEVELOPMENT

Duration: Day 21 – Day 25

1. Introduction

Python Application Development is the process of creating applications using Python. It is used for web development, APIs and database applications.

2. Flask Framework

Flask is a lightweight Python web framework used to develop web applications and APIs.

Installation:

pip install flask

Program 1: Basic Flask Application

from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Welcome to Flask"

if __name__ == '__main__':
    app.run(debug=True)

3. Routing and Endpoints

Routing connects URLs to functions. Endpoints are URLs used to access application resources.

Program 2: Multiple Routes

from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Home Page"

@app.route('/about')
def about():
    return "About Page"

if __name__ == '__main__':
    app.run(debug=True)

4. HTTP Methods

- GET – Retrieve data.
- POST – Insert data.
- PUT – Update data.
- DELETE – Delete data.

5. SQLite Database

SQLite is a lightweight database used to store information. Python uses the sqlite3 module to connect with it.

Program 3: Create Database

import sqlite3

con = sqlite3.connect("student.db")
con.execute("""CREATE TABLE IF NOT EXISTS students(
id INTEGER PRIMARY KEY,
name TEXT,
age INTEGER)""")
con.commit()
con.close()

print("Database Created Successfully")

6. CRUD Operations

CRUD means Create, Read, Update and Delete.

Program 4: Insert Record

import sqlite3

con = sqlite3.connect("student.db")
con.execute("INSERT INTO students(name,age) VALUES(?,?)",
("Lasya",18))
con.commit()
con.close()

print("Record Inserted")

Program 5: Display Records

import sqlite3

con = sqlite3.connect("student.db")
cur = con.execute("SELECT * FROM students")

for row in cur:
    print(row)

con.close()

Program 6: Update Record

import sqlite3

con = sqlite3.connect("student.db")
con.execute("UPDATE students SET age=19 WHERE id=1")
con.commit()
con.close()

print("Record Updated")

Program 7: Delete Record

import sqlite3

con = sqlite3.connect("student.db")
con.execute("DELETE FROM students WHERE id=1")
con.commit()
con.close()

print("Record Deleted")

7. API Authentication

Authentication checks whether a user is allowed to access an application.

Program 8: Basic Authentication

from flask import Flask, request
app = Flask(__name__)

@app.route('/login')
def login():
    token = request.headers.get('Authorization')

    if token == "mysecret123":
        return "Access Granted"

    return "Unauthorized", 401

if __name__ == '__main__':
    app.run(debug=True)

8. Schema Validation

Schema validation checks whether received data follows the required format, such as name as text and age as a number.

9. REST API

REST API allows two applications to communicate using HTTP methods and JSON data.

10. API Testing

API testing checks whether an API works correctly. Tools include Postman and Thunder Client.

11. MINI PROJECT – STUDENT MANAGEMENT API

Aim: To create a Student Management API using Python Flask and SQLite.

Features:

1. Add student details.
2. View student details.
3. Update student details.
4. Delete student details.

Project Code:

from flask import Flask, request
import sqlite3

app = Flask(__name__)

def db():
    return sqlite3.connect("students.db")

con = db()
con.execute("""CREATE TABLE IF NOT EXISTS students(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT, age INTEGER, branch TEXT)""")
con.commit()
con.close()

@app.route('/')
def home():
    return "Student Management API"

@app.route('/students', methods=['POST'])
def add():
    data = request.get_json()
    if not isinstance(data, dict):
        return {"error": "Invalid data"}, 400

    name = data.get('name')
    age = data.get('age')
    branch = data.get('branch')

    if not isinstance(name, str) or not name.strip():
        return {"error": "Invalid name"}, 400
    if type(age) != int or age <= 0:
        return {"error": "Invalid age"}, 400
    if not isinstance(branch, str) or not branch.strip():
        return {"error": "Invalid branch"}, 400

    con = db()
    con.execute("INSERT INTO students(name,age,branch) VALUES(?,?,?)",
                (name,age,branch))
    con.commit()
    con.close()
    return {"message": "Student Added"}

@app.route('/students', methods=['GET'])
def view():
    con = db()
    con.row_factory = sqlite3.Row
    rows = con.execute("SELECT * FROM students").fetchall()
    con.close()
    return [dict(row) for row in rows]

@app.route('/students/<int:id>', methods=['PUT'])
def update(id):
    data = request.get_json()
    if not isinstance(data, dict):
        return {"error": "Invalid data"}, 400

    name = data.get('name')
    age = data.get('age')
    branch = data.get('branch')

    if not isinstance(name, str) or not name.strip():
        return {"error": "Invalid name"}, 400
    if type(age) != int or age <= 0:
        return {"error": "Invalid age"}, 400
    if not isinstance(branch, str) or not branch.strip():
        return {"error": "Invalid branch"}, 400

    con = db()
    cur = con.execute(
        "UPDATE students SET name=?,age=?,branch=? WHERE id=?",
        (name,age,branch,id))
    con.commit()
    con.close()

    if cur.rowcount == 0:
        return {"error": "Student Not Found"}, 404
    return {"message": "Student Updated"}

@app.route('/students/<int:id>', methods=['DELETE'])
def delete(id):
    con = db()
    cur = con.execute("DELETE FROM students WHERE id=?", (id,))
    con.commit()
    con.close()

    if cur.rowcount == 0:
        return {"error": "Student Not Found"}, 404
    return {"message": "Student Deleted"}

if __name__ == '__main__':
    app.run(debug=True)

12. How to Run

1. Install Flask using "pip install flask".
2. Save the project as "app.py".
3. Run "python app.py".
4. Open "http://127.0.0.1:5000/".
5. Test API operations using Postman.

13. Daily Work Plan

- Day 21: Flask basics and routing.
- Day 22: SQLite and CRUD operations.
- Day 23: Authentication and validation.
- Day 24: Student Management API project.
- Day 25: Testing and submission.

14. Deliverables

1. GitHub Repository – Upload project code.
2. Learning Notes – Submit notes and programs.
3. LinkedIn Post – Share project and learning experience.

Conclusion

Through this module, I learned Flask, SQLite, CRUD operations, API authentication, validation and REST API development. I also developed a basic Student Management API using Python.# Python-application-development-