# Flask Framework :

- Flask framework is used to build end-to-end web application
- It is a complete Web Framework created with the help of Python prograaming language

- 2 IMP components :
    1. WSGI - Web Server Gateway Interface
    2. Jinja2 - Template Engine

1. WSGI :
    - Web Servers :
        - AWS EC2
        - Azure APP
        - APACHE

    Requests -> `WEB SERVER` <-- WSGI PProtocal --> `Web App` (Built using flask framework)

2. Jinja2 Template Engine :
    - Connects web templates with a data source
    - a data source can be :
        - SQL DB
        - MongoDB
        - ML model
    - useful in creating dynamic web pages

## Practical implementation of Flask 

```bash
pip install flask
```

#### app.py
```py
from flask import Flask

# create an instance of Flask app (WSGI application)
app = Flask(__name__)

# Create a Home page
@app.route("/") # displayed in url after the domain name
def welcome():
    return "Welcome to Flask web app"

# Create another page
@app.route("/index") # will open a new page and display "/index" after the domain name
def index():
    return "This is the index Page."

#create entry point for the application :
if __name__ == "__main__" :
    # app.run() this will start the web app
    app.run(debug=True)
```
- We have to again close the app and then restart it again to see the changes made while the dvelopment.
- So to see the changes without having to restart the app again, we will have to set `debug = True` in `app.run()` => `app.run(debug=True)`

- We can also return HTML code :
```python
@app.route("/index")
def index():
    return "<html><h1> Welcome to H1 of flask app </h1></html>"
```

- But we have to write a lot of html code, so this is not the best practice to do so.
- What we can do alternatively is that we can pass an html file using `render_template(index.html)` method instead.

```py
from flask import Flask, render_template

@app.route("/index")
def index():
    return render_template("index.html")
```

### What the `render_template()` do ?
- inside the parent folder, it looks for another folder named `templates`.
- then it searches for the file in that folder.

### Directory Structure in Python :
- The directory structure in Flask should have the `static` folder and a `templates` folder in the parent folder where the main file `app.py` is present.
- This requirement is compulsory
- we should avoid spelling mistakes and subfolders while developing this directory structure.

    ![Directory structure](image.png)

1. `static` folder :
    - it is used to store the files which are to be rendered directly.
    - if we add a `demo.txt` file in the static folder, and then we hit the url like : `abc@domain.com/static/demo.txt` then we will be able to see the contents of the file in the web page directly.
    - We can simply open the url `abc@domain.com/static/` but we will not be able to open that directory in the webpage. But if we again give a file path present in the static folder, it will open it for us.
    - If the file cannot be display in the browser, it will directly **download** it for us. 

2. `templates` folder :
    - this folder stores all the HTML files(templates)
    - the `render_template()` function in flask searches for the HTML template files in the `templates` folder.
    
     
## HTTP VERBS :
- There are 4 main HTTP verbs :
    1. `GET`
    2. `POST`
    3. `PUT`
    4. `DELETE`

1. `GET` Method :
    - The get 
