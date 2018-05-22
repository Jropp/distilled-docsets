# Webpack

## Core Concepts

Everything fits into one of these four areas

## Questions

When using html-loader, how are the bundled files extracted from main.js? Particularly the html files. 

## Entry

You can have one or multiple entry points for your project. Think of an entry point as a single file that is the trunk of a tree. You set this entry point as your trunk and then connect all the branches that you need from there. 

So you might have a main.js file that imports all sorts of other js files, into it with something like

`import otherfile.js`

or 

`require('otherfile.js)`

I don't entirely understand import or require syntax so make sure to double check formatting.

But WP will detect those branches automatically and bundle them all into one file for you.

## Output

The default of WP is to create and bundle the files into a dist/ folder in the root of your project

## Loaders

The default for WP is bundling js files. But there are loaders to bundle other types of files.

Loaders transform source code into javascript, or inline images into data URLs.

They are like 'tasks' if you have used other build tools.

### Setup/Configuration

You can use loaders one of three ways:

- In the webpack.config.js file
- Inline in your code in each import statement
- In the command line

I have stuck to using them in webpack.config.js (see example in html-loader)


### html-loader

The following bundled the html properly into nodes in the bundle.js (I think it did anyway). To date I haven't figured out how to get the page to display properly though.

```
// note: The module property here is sibling to entry, output, and plugin properties
module: {
		rules: [
			{
				test: /\.html$/,
				use: [
					{
						loader: "html-loader",
						options: {
							name: '[name].[ext]',
							outputPath: "/",
							minimize: true,
							attrs: ['link:href', 'script:src']
						}
					}
				],
				// this code is because below in the project at this point I was using an HTMLwebpackplugin to copy the homepage into the dist folder
				exclude: path.resolve(__dirname, 'src/index.html')
			},
			{
				test: /\.css$/,
				use: ['style-loader', 'css-loader']
			},
			{
				test: /\.js$/,
				use: 'babel-loader'
			},
		]
```
## Plugins

Other open source npm tools to help you do what you need. 

### HTMLWebpackplugin

I used this on my [onboarding project](https://github.com/Jropp/jason-ropp-js-iobp/pull/35) at one point. It creates a new entry point for an html file. At first I used a new plugin for each html file and things worked properly. But this got clunky. 

It looked like this:

```
plugins: [
  // This was my homepage
		new HtmlWebPackPlugin({
      // Not sure what this hash is for, it worked even without it
			hash: true,
			template: "src/index.html",
			filename: "index.html"
		}),
		new HtmlWebPackPlugin({
			template: "./src/components/edit-user.html",
			filename: "./edit-user.html"
		}),
		new HtmlWebPackPlugin({
			template: "./src/components/new-user.html",
			filename: "./new-user.html"
		}),
		new HtmlWebPackPlugin({
			template: "./src/components/user-profile.html",
			filename: "./user-profile.html"
		}),
		new HtmlWebPackPlugin({
			template: "./src/components/users-list.html",
			filename: "./users-list.html"
		}),

    // This is a polymer custom element
		new HtmlWebPackPlugin({
			template: "./src/components/nav-bar.html",
			filename: "./nav-bar.html"
		}),

    // this is the root file for @banno/polymer
		new HtmlWebPackPlugin({
			template: "./node_modules/@banno/polymer/polymer.html",
			filename: "./polymer.html"
		})
	]
```