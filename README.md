![Banner](https://github.com/Dhananjayan-PN/Django-React-Setup-Guide/blob/main/Django%20%26%20React.png "Django & React")

# Django-React-Setup-Guide
A guide to setup a React frontend with a Django backend

# Pre-requisites
A basic understanding of Python, Django, JavaScript & React

# Steps
1. Install Django: `pip(3) install django`

2. Install Virtualenv: `pip(3) install virtualenv`

3. Start Django Project: `django-admin startproject djangoreact`

4. Start virutalenv in project: `cd djangoreact && python3 -m virtualenv env`

5. Activate virtualenv: `source env/bin/activate` on Mac or `env\Scripts\activate` on Windows

6. Install Packages in Virtualenv: `pip install django`

7. Start Django Frontend App: `django-admin startapp frontend`

8. Add `'frontend'` to the `INSTALLED_APPS` list in `djangoreact/djangoreact/settings.py` file

9. Setup urls.py in `djangoreact/djangoreact/urls.py` to include frontend urls:
    * Add an import statement `from django.urls import include`
    * To the `urlpatterns` list add: `path('', include('frontend.urls')),`

10. Create a `templates` folder in the `frontend` app folder & in the `templates` folder create a `frontend` folder

11. In `frontend/templates/frontend` create an `index.html` file and enter the following:
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Django React</title>
        {% load static %}
      </head>
      <body>
        <div id="root"></div>
        <script src="{% static "js/main.js" %}"></script>
      </body>
    </html>
    ```

12. Create a `static` folder in the `frontend` app folder and add 3 subfolders: `css`, `js` & `images`

13. In `djangoreact/djangoreact/settings.py` file change STATIC_URL from `/static/` to `/frontend/static/`

14. In the `frontend/views.py` file, create a view like the following:
    ```python
    from django.shortcuts import render
    
    def index(request):
        return render(request, 'frontend/index.html')

15. Create a `urls.py` file in `frontend` app folder and enter the following in it:
    ```python
    from django.urls import path
    from .views import index

    urlpatterns = [
        path('', index),
    ]
    ```
    
Now onto some React & Webpack config
 
16. Create a folder called `src` in the `frontend` app folder and create an `index.js` file and a `components` subfolder in this `src` folder
 
17. Install npm & node from [here](https://nodejs.org/en/)
 
18. Make sure for the following commands you are inside the `frontend` app directory
 
19. Initialize an npm project: `npm init -y`
 
20. Now install Webpack, Babel and React through the following npm commands:

    `npm install webpack webpack-cli --save-dev`
    
    `npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev`
    
    `npm install @babel/plugin-proposal-class-properties` (for implementing async/await in our React components)
    
    `npm install react react-dom --save-dev`
    
21. Create a file called `babel.config.json` in the `frontend` app directory and write as shown [here](https://github.com/Dhananjayan-PN/Django-React-Setup-Guide/blob/main/babel.config.json)

22. Create a file called `webpack.config.js` in the `frontend` app directory and write as shown [here](https://github.com/Dhananjayan-PN/Django-React-Setup-Guide/blob/main/webpack.config.js)

23. Modify the npm scripts in the `package.json` file in the `frontend` app directory:
    1. Remove `"test": "echo \"Error: no test specified\" && exit 1"` from the scripts object
    2. Add `"dev": "webpack --mode development --watch",`
    3. Add `"build": "webpack --mode production",`
    4. Save file

24. Create a file called `App.js` in the `src/components` folder we created and write the following:
    ```javascript
    import React from "react";

    const App = (props) => {
      return (
        <div className="App">
          <h1>Django React Setup Works</h1>
        </div>
      );
    };

    export default App;
    ```
    
25. Enter the following in the `src/index.js` file:
    ```javascript
    import React from "react";
    import ReactDOM from "react-dom";
    import App from "./components/App";

    ReactDOM.render(
      <React.StrictMode>
        <App />
      </React.StrictMode>,
      document.getElementById("root")
    );
    ```
    
26. In the terminal, `cd` to the project root directory and enter `python manage.py migrate && python manage.py runserver`

27. In a new terminal window, execute `cd frontend && npm run dev`

28. Visit [http://127.0.0.1:8000](http://127.0.0.1:8000) in your web browser and you should see your Django React Setup Works page.

29. Edit `App.js` file to whatever you want it to say. Save the file & reload on the browser to see your changes!

30. Happy Coding!

### Now you can get building some crazy React frontend with a powerful Django backend 😎

