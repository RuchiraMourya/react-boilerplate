This is the react project starter using webpack, babel, npm (without using create-react-app )

Folder Structure:

mkdir react-boilerplate
cd react-boilerplate

Initialize the Project:

npm init 

You’ll be asked few questions related to the project, you can skip them by pressing enter, if you want to skip all the questions, add a -y flag.

 npm init -y

Installing Webpack: 

Webpack is a module bundler that lets us bundle our project files into a single file for production.

npm install webpack webpack-cli --save-dev

Installing React:

npm install react react-dom --save

Installing Babel:

npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev


Preset is a set of plugins used to support particular language features. For example, env preset helps babel to transpile es7, es6 code to es5, and react preset adds support for JSX.

Without the Presets, babel will only transfer files from one folder to another, but it can’t transpile the code.

Index.js :

Create an index.js file inside root of the /src folder.

Index.html :

Create an index.html file inside root of the /src folder and add following code inside it.

Entry and Output file:

Create a webpack.config.js in the root directory of the project so that we can define rules for our loaders.

const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "index_bundle.js"
  }
};

Webpack Loaders:
Now add some loaders inside this file, which will be responsible for loading and bundling the source files.

Here babel-loader is used to load our JSX/JavaScript files and css-loader is used to load and bundle all of the CSS files into one file and style-loader will add all of the styles inside the style tag of the document.

Install css-loader and style-loader:
npm install css-loader style-loader --save-dev


const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "index_bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  }
};

.babelrc:
Now create a .babelrc file inside root of the project directory with the following contents inside of it.

{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}

Compiling files using Webpack:
"start": "webpack --mode development --watch",
"build": "webpack --mode production"

App.js:
Create an App.js file inside the components folder of the src folder with the following contents inside of it.

import React, { Component } from "react";

import '../styles/App.css';

class App extends Component {
    render() {
        return (
            <div>
                <h1>My React App!</h1>
            </div>
        );
    }
}

export default App;


App.css:
Create an App.css file inside the styles folder of the src folder with the following contents inside of it.

h1 {
    color: #27aedb;
    text-align: center;
}

modify the index.js file
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App.js";

ReactDOM.render(<App />, document.getElementById("root"));

Installing Html-webpack-plugin:

Now we also need to install html-webpack-plugin, this plugin generates an HTML file, injects the script inside the HTML file and writes this file to dist/index.html.

npm install html-webpack-plugin --save-dev

configure in webpack config:
 plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html"
    })
  ]

  Installing Webpack-dev-server:
Install webpack-dev-server as a dev-dependency

npm install webpack-dev-server --save-dev
And change the package.json start script like below:

"start": "webpack-dev-server --mode development --open --hot"
I have added two flags --open and --hot which opens and refreshes the web page whenever any change is made to components.

Now run the below command in the terminal:

npm start

Its done :-)
