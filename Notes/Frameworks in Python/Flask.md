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

```py
@app.route("/index", methods = ['GET'])
def index() :
    return render_template('index.html')
```

```py
from flask import Flask, render_template, request 
## `request` method is used to access the method used

@app.route("/form", methods = ['GET', 'POST'])
def form():
    if request.method == 'POST' :
        name = request.form['name'] ## the id of the input tag for name should be set to 'name'
        return f'Hello {name}'
    return render_template("form.html")

```

*form.html*
```html
<html>
    <head></head>
    <title></title>
    <body>
        <form method="post">
            <label for="name">Name :</label>
            <input type="text" id="name" name="name">
            <input type="submit" value="Submit">
        </form>
    </body>
</html>
```

- form `action` :

we can actually set the attribute of the `<form>` tag in html page to a url and the app then routes to that url once the submit button is clicked :

- *form.html*
```html
<html>
    <body>
        <form action="/submit">
            <label for="name">Name :</label>
            <input type="text" id="name" name="name">
            <input type="submit" value="Submit">
        </form>
    </body>
</html>
```

```py
@app.route("/submit")
def submit():
    if request.method == 'POST' :
        name = request.form['name'] ## the id of the input tag for name should be set to 'name'
        return f'Hello {name}'
    return render_template("form.html")
```

## Variable Rule  :

```py
@app.route("/success/<score>")
def success(score):
    return "You got a score of : " + score
```

- here when you type in the url : `main_url_path/success/55` :
the value 55 will be passed to the value of the variable `score`.
- however, by default it is passed as the string.

- if we want to pass it as an integer, we need to declare the type of the variable `score` :
```py
@app.route("/success/<int:score>") ## Specified the type of the variable
def success(score) :
    return "You got a score of : " + str(score) ## Typecasting the int to str is needed while concatenating
```


## Building URL Dynamically :
- we saw how we can pass the `score` value into the retirn statement.
- But if we were to return an html page using `render_template()`, and the results value in the html page should be extracted from variable `score`, then we need to :

```py
@app.route("/success/<int:score>")
def success(score):
    res = ""
    if score > 35 :
        res = "PASS"
    else : 
        res = "FAIL"

    return render_template("results.html", results = res)
```

```html
<html>
    <body>

        <h1>

            Based on the marks you have {{ results }}

        </h1>
    </body>
</html>
```

## Jinja 2 Template Engine :

- `{{ }}` -- expressions to print output in html
- `{%...%}` -- coditions, for loops
- `{#...#}` -- comments

```py
@app.route("/success/<int:score>")
def success(score):
    res = ""
    if score > 35 :
        res = "PASS"
    else : 
        res = "FAIL"

    exp = {'score' : score, 'res' : res}

    return render_template("results.html", results = exp)
```

```html
<html>
    <h2>

        Final results
    </h2>
    <body>
        <table border=2>
            {% for key, value in results.items() %}
            <tr>

                <td> {{ key }} </td>
                <td> {{value}} </td>
            </tr>
            {% endfor %}
        </table>
    </body>
</html>
```

```html
<h1>
    
    {% if results >= 50 %}
    <p> You have passed with marks {{ results }}</p>
    {% else %}
    <p> You failed with marks : {{ results }}</p>
    {% endif %}
</h1>
```

- Now, if we want to redirect from a page based on a condition -- Lets say, if score is greater than 50, redirect to `/success` page. else redirect to `/fail` page.

- for this, we need to import 2 more functions : `redirect()` and `url_for()`

```py
from flask import redirect, url_for

@app.route("/success/<int:score>")
def success(score) :
    return f"you passed with score : {score}"

@app.route("/fail/<int:score>")
def fail(score) :
    return f"You Failed with score : {score}"

@app.route("/submit", methods = ['POST', 'GET'])
def submit():
    total_score = 0
    if request.method == 'POST' :
        science = float(request.form['science'])
        maths = float(request.form['maths'])
        c = float(request.form['c'])
        data_science = float(request.form['data_science'])

        total_score = (science + maths + c + data_science)/4
    else :
        return render_template('get_results.html')

    return redirect(url_for("success", score = total_score))
```

## To-Do List app :

- All methods -- GET, POST, PUT, DELETE


```py
from flask import Flask, jsonify, request

app = Flask(__name__)

## Initialise data in my to-do list
items = [
    {"id" : 1, "name": "Item 1", "description" : "This is item 1"},
    {"id" : 2, "name": "Item 2", "description" : "This is item 2"}
]

@app.route("/")
def home():
    return "Welcome to the Sample To-do List APP"

## GET : Retrieve all the items :
@app.route("/items", methods = ["GET"])
def get_items():
    return jsonify(items)

## GET : Retrieve a specific item by ID :
@app.route("/items/<int:item_id>", methods = ["GET"])
def get_item(item_id):
    item = next((for item in items if item["id"]== item_id), None)

    if item is None:
        return jsonify({"error" : "item not found"})
    return jsonify(item)

## POST : Create a new task
@app.route("/items", methods = ["POST"])
def create_item():
    if not request.json or not 'name' in request.json :
        return jsonify({"error" : "item not found"})
    new_item = {
        "id" : items[-1]["id"] + 1 if items else 1,
        "name" : request.json['name'],
        "description" : request.json["description"]
    }

    items.append(new_item)
    return jsonify(new_item)

## PUT : Update existing item 
@app.route("/items/<int:item_id>", methods = ["PUT"])
def update_item(item_id):
    item = next((item for item in items if item["id"] == item_id), None)

    if item is None:
        return jsonify({"error" : "Item not found"})
    item["name"] = request.json.get('name', item['name'])
    item["description"] = request.json.get('description', item['description'])

    return jsonify(item)

## DELETE : Delete an item
@app.route('/items/<int:item_id>', methods = ['DELETE'])
def delete_item(item_id):
    global items
    items = [item for item in items if item["id"] != item_id]
    return jsonify({"result" : "item deleted"})
```