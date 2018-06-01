# HTMLWebpackPlugin

## Basics

Generates an HTML5 file that includes all of your webpack bundles in the body.

The script tag should be generated automatically with the proper path to your bundled files.

```
new HtmlWebPackPlugin({
			hash: true,
			template: "src/index.html",
			filename: "index.html"
		}),
```
###### Example Comments

- not sure what the hash is for
- the plugin creates a new file, but setting the template means it will copy whatever the template is