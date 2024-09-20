<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Navbar Toggle with Tailwind CSS and Flask</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
        }
        h1, h2, h3 {
            color: #4A5568;
        }
        code {
            background-color: #F7FAFC;
            padding: 2px 6px;
            border-radius: 4px;
            font-family: Consolas, monospace;
            color: #2D3748;
        }
        pre {
            background-color: #EDF2F7;
            padding: 10px;
            border-radius: 4px;
            overflow-x: auto;
        }
        .code-block {
            background-color: #F7FAFC;
            padding: 15px;
            border-left: 4px solid #4A5568;
        }
    </style>
</head>
<body>

    <h1>Navbar Toggle with Tailwind CSS and Flask</h1>

    <p>This project demonstrates how to create a collapsible sidebar (navbar) using Tailwind CSS in a Flask web application. The navbar dynamically changes width, hides the text logo, and updates the direction of an arrow icon when toggled. The project integrates Tailwind CSS with a Flask backend to manage the assets.</p>

    <h2>Features</h2>
    <ul>
        <li>Collapsible sidebar using Tailwind CSS.</li>
        <li>Navbar width toggles between <code>w-60</code> and <code>w-20</code>.</li>
        <li>Hides/shows a text logo (<code>UNIVERSITY</code>) when toggled.</li>
        <li>Changes the direction of an arrow (<code>←</code> or <code>→</code>) dynamically when the sidebar is expanded or collapsed.</li>
        <li>Fully responsive using Tailwind's utility classes.</li>
    </ul>

    <h2>Prerequisites</h2>
    <ul>
        <li>Basic knowledge of <strong>HTML</strong>, <strong>CSS</strong>, and <strong>JavaScript</strong>.</li>
        <li>Familiarity with <strong>Flask</strong> as a web framework.</li>
        <li>Understanding of <strong>Tailwind CSS</strong> utility-based framework.</li>
    </ul>

    <h2>Concepts Used</h2>
    
    <h3>1. Tailwind CSS</h3>
    <p>Tailwind CSS is a utility-first CSS framework that provides low-level utility classes to build custom designs directly in your HTML. Instead of writing custom CSS for styling, Tailwind provides a set of predefined classes that help you quickly apply specific styles, such as margins, padding, colors, fonts, and layout utilities.</p>

    <h4>Key Tailwind Concepts Used:</h4>
    <ul>
        <li><strong>Utility Classes</strong>: Classes like <code>w-60</code>, <code>w-20</code>, <code>h-screen</code>, <code>bg-purple-600</code>, <code>hidden</code>, etc., are predefined in Tailwind CSS.</li>
        <li><strong>Responsive Design</strong>: Tailwind makes it easy to create responsive designs by providing mobile-first utilities.</li>
        <li><strong>Flexbox Utilities</strong>: Tailwind offers easy-to-use flex utilities for managing layout (e.g., <code>flex</code>, <code>justify-center</code>, etc.).</li>
        <li><strong>Transitions</strong>: To provide smooth animations for expanding and collapsing the navbar, classes like <code>transition-all</code> and <code>duration-300</code> were used.</li>
    </ul>

    <h3>2. JavaScript DOM Manipulation</h3>
    <p>JavaScript is used to toggle classes on elements to change the width of the navbar, show/hide the logo, and update the arrow icon.</p>

    <h4>JavaScript Functions:</h4>
    <ul>
        <li><strong>toggleNavbar()</strong>: Toggles between the expanded and collapsed state of the navbar. It also switches the arrow direction and hides the logo text when the navbar is collapsed.</li>
    </ul>

    <h3>3. Flask</h3>
    <p>Flask is a lightweight Python web framework used for managing the backend of this project. Flask will serve the HTML page that includes the Tailwind CSS and JavaScript for the interactive navbar.</p>

    <h2>Project Structure</h2>
    <pre class="code-block">
├── app.py                     # Flask backend
├── static
│   ├── css
│   │   └── main.css            # Compiled Tailwind CSS
├── templates
│   └── index.html              # Main HTML page with Tailwind classes
└── README.md                   # Project readme file
    </pre>

    <h2>How to Set Up Tailwind CSS in a Flask Web App</h2>

    <h3>Step 1: Set Up Flask</h3>
    <p>Create a basic Flask application structure:</p>
    <pre class="code-block">
mkdir flask_tailwind_navbar
cd flask_tailwind_navbar
python3 -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
pip install flask
    </pre>

    <p>Create <code>app.py</code>:</p>
    <pre class="code-block">
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)
    </pre>

    <h3>Step 2: Install Tailwind CSS</h3>
    <p>You can use Tailwind CSS via <strong>CDN</strong> or <strong>locally</strong>. Here's how to use it with Flask:</p>

    <h4>Option 1: Using the Tailwind CDN</h4>
    <p>In your <code>index.html</code>, add the Tailwind CDN in the <code>&lt;head&gt;</code> section:</p>
    <pre class="code-block">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
    </pre>

    <h4>Option 2: Setting Up Tailwind Locally</h4>
    <ol>
        <li>Install <strong>Node.js</strong> if you don't already have it.</li>
        <li>Install Tailwind CSS via npm:</li>
        <pre class="code-block">npm install -D tailwindcss</pre>
        <li>Configure the Tailwind setup:</li>
        <pre class="code-block">
npx tailwindcss init
        </pre>
        <li>Create a Tailwind configuration file:</li>
        <pre class="code-block">
module.exports = {
  content: [
    './templates/**/*.html',
    './static/**/*.js',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
        </pre>
        <li>Create a CSS file (<code>static/css/main.css</code>) and include Tailwind's base, components, and utilities:</li>
        <pre class="code-block">
@tailwind base;
@tailwind components;
@tailwind utilities;
        </pre>
        <li>Compile the Tailwind CSS:</li>
        <pre class="code-block">npx tailwindcss -i ./static/css/main.css -o ./static/css/output.css --watch</pre>
        <li>Link the compiled CSS file in your HTML:</li>
        <pre class="code-block">
<link rel="stylesheet" href="{{ url_for('static', filename='css/output.css') }}">
        </pre>
    </ol>

    <h3>Step 3: Create <code>index.html</code></h3>
    <p>Place your HTML inside the <code>templates/</code> folder:</p>
    <pre class="code-block">
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="{{ url_for('static', filename='css/output.css') }}">
    <title>Document</title>
</head>
<body>

    <div class="flex">
        <div id="toggleNav" class="w-60 h-screen p-2 pt-4 bg-purple-600 relative flex transition-all duration-300">
            <h1 class="text-xl text-white">AKS <span id="logo" class="inline-block">UNIVERSITY</span></h1>
            <div id="arrow" class="pb-2 pt-1 pl-3 w-12 bg-white rounded-full text-3xl font-bold text-purple-600 absolute -right-6 cursor-pointer"
                onclick="toggleNavbar()">←</div>
        </div>
        <div class="flex-1 p-4">
            <h2>Dashboard Content Here</h2>
        </div>
    </div>

    <script>
        function toggleNavbar() {
            var nav = document.getElementById('toggleNav');
            var logo = document.getElementById('logo');
            var arrow = document.getElementById('arrow');

            if (nav.classList.contains('w-60')) {
                nav.classList.remove('w-60');
                nav.classList.add('w-20');
                logo.classList.add('hidden');
                arrow.innerHTML = '→';
            } else {
                nav.classList.remove('w-20');
                nav.classList.add('w-60');
                logo.classList.remove('hidden');
                arrow.innerHTML = '←';
            }
        }
    </script>

</body>
</html>
    </pre>

    <h2>Conclusion</h2>
    <p>This project is a simple demonstration of how to use Tailwind CSS and Flask to create a collapsible sidebar navigation that is responsive and interactive. The code can be further enhanced to include more navigation links, icons, and dynamic features based on your project needs.</p>

</body>
</html>
