# Writing a Loader

Definition: A loader is a [node module](https://www.w3schools.com/nodejs/nodejs_modules.asp) that exports a function.

That function is called when a resource (lets say myfile.html for the sake of this documentation) needs to be transformed by the particular loader.

## Setup Options

### 1 Test a single loader

In webpack.config.js:
```
{
  test: /\.js$/
  use: [
    {
      loader: path.resolve('path/to/loader.js'),
      options: {/* ... */}
    }
  ]
}
```

### 2 Test multiple loaders

### 3 Create separate repo and package

`npm link` it to the project in which you want to test it

## [Basics](https://webpack.js.org/contribute/writing-a-loader/#simple-usage)

When a single loader is applied to myFile.html, the loader (remember its a function) has one parameter: a string containing the content of myFile.html.

An example:

This is an actual bundled html file from a project that I did.

```
/***/ "./src/components/users-list.html":
/*!****************************************!*\
  !*** ./src/components/users-list.html ***!
  \****************************************/
/*! no static exports found */
/***/ (function(module, exports, __webpack_require__) {

eval("module.exports = \"<!DOCTYPE html> <html lang=en> <head> <meta charset=utf-8 /> <meta http-equiv=X-UA-Compatible content=\\\"IE=edge\\\"> <title>Users List</title> <meta name=viewport content=\\\"width=device-width,initial-scale=1\\\"> <link rel=import href=\" + __webpack_require__(/*! ./nav-bar.html */ \"./src/components/nav-bar.html\") + \"> </head> <body> <header> <nav> <nav-bar></nav-bar> </nav> </header> <h1> Users: </h1> <ul> <li> <hgroup class=user-card> <h2 class=name>Jason Ropp</h2> <h3 class=id>ID: Wombat</h3> <h3 class=phone>541-615-9999</h3> <h3 class=email> <a href=dummy@email.com>dummy@email.com</a> </h3> <button type=button onclick=toggleUserDetails(event)>Hide Details</button> </hgroup> </li> </ul> </body> <script> 'use strict';\\n\\n  let toggleDisplay = function(elem) {\\n    // Bug Fix: The first instance on page load\\n    // does not register the display block style,\\n    // even when added explicitly in main.css.\\n    if (elem.style.display === '') {\\n      elem.style.display = 'none';\\n    } else {\\n      elem.style.display = (elem.style.display === 'block') ? 'none' : 'block';\\n    }\\n  };\\n\\n  let toggleUserDetails = function(event) { // eslint-disable-line no-unused-vars\\n    let userElems = Array.prototype.slice.call(event.target.parentNode.children);\\n\\n    for (let i = 0; i < userElems.length; i++) {\\n      let elem = userElems[i];\\n\\n      if (elem.nodeName === 'H3') {\\n        toggleDisplay(elem);\\n      }\\n    }\\n  }; </script> </html> \";\n\n//# sourceURL=webpack:///./src/components/users-list.html?");

/***/ }),
```

**Synchronous loaders** can simply return a single value: the transformed module. 

Q: Does 'transformed module' mean the module transformed into a string, or the string transformed back into code when you serve the project. 

## Complex Loaders

- Multiple loaders are chained and they execute in reverse order