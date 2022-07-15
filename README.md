# Webpack Template

I usually start my projects not using package manager bacause, as you know, node_modules is the heaviest object on the universe. 

As you can see [here](#dev-dependencies), Im not using sass-loader because I use `sass --watch` to compile my `.scss` file to `.css` file. Also, I just use VSCode Live Server Extension not `webpac-dev-serve` during my development.

This is just my webpack template to bundle javascript modules for my small project to run on github.

## Getting Started

  - create "src" folder (here goes your development code)
  - init package.json
    ```
    npm init -y
    ```
  - [Install Dev Dependencies](#dev-dependencies)
  - create a "build" script command with a value of "webpack build" on package.json 
    ```json
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build": "webpack build", // <--
    },
    ```
  - create [Webpack Config](#webpack-config-file) on the root folder - webpack.config.js
  - [configure src](#configure-source-files) your `index.html` and `main.js` file
  - Run Build
    ```
    npm run build
    ```
  - create [.gitignore](#gitignore) file

### Configure Source files

  - On your `index.html` file, comment out the link:css and script:src
  - On your `main.js` file, import your style at the very top. ()
    ```
    import "../styles/main.css";
    ```

  After the above steps, we dont have any styles and js on VSCode Live Server Extension.

### Dev Dependencies

  - webpack & webpack-cli
    ```
    npm install -D webpack webpack-cli
    ```
  - html-loader html-webpack-plugin
    ```
    npm install -D html-loader html-webpack-plugin
    ```
  - style-loader css-loader
    ```
    npm install -D style-loader css-loader
    ```

  or

  - Combine all
    ```
    npm install -D webpack webpack-cli html-loader html-webpack-plugin style-loader css-loader
    ```

### Webpack Config File

  ```js
  const path = require('path');
  const HtmlWebpackPlugin = require('html-webpack-plugin');

  module.exports = {
    mode: 'production',
    entry: path.resolve(__dirname, 'src/javascripts/main.js'),
    output: {
      filename: 'main.js',
      path: path.resolve(__dirname, 'dist'),
      assetModuleFilename: 'images/[name][ext]',
    },
    module: {
      rules: [
        {
          test: /\.html$/,
          use: ["html-loader"],
        },
        {
          test: /\.css$/,
          use: ["style-loader", "css-loader"]
        },
        {
          test: /\.(png|svg|jpg|jpeg|gif)$/i,
          type: 'asset/resource', 
        },
      ]
    },
    plugins: [
      new HtmlWebpackPlugin({
        template: path.resolve(__dirname, 'src/index.html'),
        filename: 'index.html',
      }),
    ]
  }
  ```

### gitignore

When using git as version control, you don't want to include "node_modules" package on your commits.

To do that, just create ".gitignore" file. On commit, git will check in this file for any file that should be ignore. Then type `node_modules/*` inside the .gitignore file then save. Thats it.