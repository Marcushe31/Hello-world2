---
toc: true
comments: true
layout: post
title: Python/Flask in Jupyter
courses: { compsci: {week: 4} }
type: hacks
---
Below are notes about Python, Flask, and Jupyter and how it relates to our coding. 

Introduction
Welcome to this journey into the world of web servers and the Flask framework! In the previous weeks, you’ve successfully set up a web server using GitHub Pages, converting Jupyter Notebooks into Markdown for a seamless online presentation. Today, we’ll take that knowledge to the next level as we dive into creating your very own web server using Flask.

Understanding Web Servers
What is a Web Server?

Traditionally, we had librarians at libraries that would help you find books or information. Today in the digital world, thousands upon thousands of home pages, search engines, and digital archives have been built using web servers.

GitHub Pages vs. Flask
You’ve already experienced a form of web server through GitHub Pages. Think of GitHub Pages as a library that has established rules for publishing Markdown notes and Jupyter Notebooks neatly on a bookshelf.

Now, let’s introduce Flask, your personal web server. Flask can create and manage any type of content, including customizing everything according to your preferences, and even serve additional information (like a database with APIs).

The Flask Framework Flask is a micro web framework written in Python. It’s designed to be minimal and easy to use, making it perfect for building web applications, APIs, and, yes, even your web server. Today, we will start with the basics of Flask and see how it empowers you to create and manage web content.

Our Goals for Today
Here’s what we’ll accomplish in this session:

Create a minimal Flask server.
Explore the Python/Flask process.
Access data from our Flask server using Python.
Access data from our Flask server using JavaScript.
Learn how to stop the Python/Flask process gracefully.
Note: Jupyter magic commmand %%python --bg that follows runs the server in background. This enables us to continue interacting with the subsequent Notebook cells.

%%python --bg

from flask import Flask, jsonify
from flask_cors import CORS

# initialize a flask application (app)
app = Flask(__name__)
CORS(app, supports_credentials=True, origins='*')  # Allow all origins (*)

# ... your existing Flask

# add an api endpoint to flask app
@app.route('/api/data')
def get_data():
    # start a list, to be used like a information database
    InfoDb = []

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "John",
        "LastName": "Mortensen",
        "DOB": "October 21",
        "Residence": "San Diego",
        "Email": "jmortensen@powayusd.com",
        "Owns_Cars": ["2015-Fusion", "2011-Ranger", "2003-Excursion", "1997-F350", "1969-Cadillac"]
    })

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "Shane",
        "LastName": "Lopez",
        "DOB": "February 27",
        "Residence": "San Diego",
        "Email": "slopez@powayusd.com",
        "Owns_Cars": ["2021-Insight"]
    })
    
    return jsonify(InfoDb)

# add an HTML endpoint to flask app
@app.route('/')
def say_hello():
    html_content = """
    <html>
    <head>
        <title>Hellox</title>
    </head>
    <body>
        <h2>Hello, World!</h2>
    </body>
    </html>
    """
    return html_content

if __name__ == '__main__':
    # starts flask server on default port, http://127.0.0.1:5001
    app.run(port=5001)

Show Python/Flask process
This script discovers the running flask process

%%script bash

