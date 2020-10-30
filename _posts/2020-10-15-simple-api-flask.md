---
layout: post
title:  "Creating a Simple API in flask"
description: "Creating a simple json API in flask"
date:   2020-10-15
---
This article assumes that you are already familiar with Flask. If not read about Flask

In this article we will create an simple API endpoint in Flask. If you want to learn how Flask handles the form here is another article for you.
### Creating HTML form

We will create a simple html form which allows users enter their name.

```html
<form method="post">
<label for="name">Your Name:</label>

  <button type="submit">Join</button>
  </form>
```

### Creating Flask App

Starting a virtual environment

```python
pip install virtualenv
python3 -m venv env
pip install flask
```

we will retrieve user entered name using Flask and append the all the names into a list

```python
# importing Flask and other modules
from flask import Flask, request, render_template

# Flask constructor
app = Flask(__name__)

# creating a python list
users = []

# A decorator used to tell the application
# which URL is associated function
@app.route('/', methods =["GET", "POST"])
def user():
	if request.method == "POST":
	# getting input with name = yourname in HTML form
	   user_name = request.form.get("yourname")
	   users.append(user_name)
	return render_template("form.html")

if __name__=='__main__':
app.run()
```

In this Flask app we will store all the user entered names in a list called users so that we will be able to serve the names in the API. Now we will add API endpoint to the Flask App.

```python
#importing jsonify
import jsonify

# creating api endpoint
@app.route('/api',methods=["GET"])
def api():
# creating dictionary with name as key and users list as value
       userapi = {"name": users }
# make dict as json by using jsonify module and passing userapi dict as argument
       return jsonify(userapi)
```

- We are creating a new route "api" which is the api end point
- In api function we create a dictionary userapi with name as key and users list as the value
- Now we return json data using jsonify module by passing userapi dictionary as argument

### Complete Flask App

```python
# importing Flask and other modules
from flask import Flask, request, render_template, jsonify

# Flask constructor
app = Flask(__name__)

# creating a python list
users = []

# A decorator used to tell the application
# which URL is associated function
@app.route('/', methods =["GET", "POST"])
def user():
	if request.method == "POST":
	# getting input with name = yourname in HTML form
	   user_name = request.form.get("yourname")
	   users.append(user_name)
	return render_template("form.html")

@app.route('/api',methods=["GET"])
def api():
       userapi = {"users": users }
       return jsonify(userapi)

if __name__=='__main__':
app.run()
```
