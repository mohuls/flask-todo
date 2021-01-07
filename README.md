# Flask to-do app

## Basic setup
1. Install Pyhton3
2. Install Python Virtual Environment
3. `$ cd /project-folder` & Create a virtual environment in the project folder as "env" with `$ virtualenv -p python3 env`
4. Activate the virtual environment `$ source env/bin/activate`
5. `$ pip3 install flask flask-sqlalchemy` install the dependencies.
5. Now create a new file called app.py and write the following most basic flask application:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
  return "Hello Flask"
  
if __name__ == "__main__":
  app.run(debug=True)
```

6. Now in the terminal run: `$ python3 app.py`. The development server should running. Browse the provided local link to see the hello world page.


## Working with Jinja templates

1. Create a folder called `templates`. Now in the template folder create `index.html` file and write something formatted in html say `<h1>Hello World</h1>`.
2. Now in the `app.py` file import a new module called `render_template` and change the return statement to `return render_template('index.html)`. The file will be look like:
```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
  return render_template('index.html')

if __name__ == "__main__":
  app.run(debug=True)
```
3. Run and browse the app, you can see the template file is working.

## Extending base template

1. Create another file in templates folder called  `base.html`. Now write the following:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  {% block head %}{% endblock %}
</head>
<body>
  {% block body %}{% endblock %}
</body>
</html>
```
2. Notice `{% block head %}{% endblock %}` and `{% block body %}{% endblock %}` is the placeholder for head and body. Or it is the base template every page will inherit just by placing the head and body section for each page. The placeholder syntax is a jinja templating syntax.
3. Now in the `index.html` replace the whole file with:
```html
{% extends 'base.html' %}

{% block head %}

{% endblock %}

{% block body %}
<h1>Hello World from Template</h1>
{% endblock %}
```
4. Here in the first line we have extended the `base.html` template.
5. In the `block head` section we will write the head section and `block body` section we will write the body section. That will be placed in the `base.html` file when the page is rendered.
6. Now browse again, you should see the The base template is also working.\

## Working with static file
1. In the static directory create a file called `css/main.css` And write the following css:
```css
body {
  margin: 0;
  font-family: sans-serif;
}
```
2. Go to `base.html` file and add the line `<link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}">` after viewport tag. Here we linked the static css file in our base head section so that every page have the file access.
3. The direct file linking is not supported in Flask. So the `url_for` module used here to link the static file. Where `static` mentions the static folder location and file name mentions the actual relative path from the static folder.
4. Browse the page again you should see the font-face and margin changed. That means the static file has been linked successfully.

**Note:** Make sure `url_for `module is imported in the app.py file.

## Working with Database
