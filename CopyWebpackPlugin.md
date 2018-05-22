# Copy Webpack Plugin

## Opening Remarks

#### Notice that all of this is happening as a plugin in your webconfig file.

## Open Questions

What is an output directory?




## Simple Pattern

Everything else below is an expansion of this
```
[
{ from: 'source', to: 'dest' }
{ from: 'source', to: 'dest' }
{ from: 'source', to: 'dest' }
]
```

Or you can just use a ‘source’ string instead of the above object and compile an array of them.

```
[
'source/of/file.html',
'nextsource/of/file.html'
]
```

If you set it up like this then you are using a default destination

If from is a directory, then to has no extension or it ends in ‘/‘

## toType:

Setup in `webpack.config.js`

### dir: 
```
[
  new CopyWebpackPlugin([
    {
      from: 'path/to/file.txt',
      to: 'directory/with/extension.ext',
      toType: 'dir'
    }
  ], options)
]
```
### file: 
```
[
  new CopyWebpackPlugin([
    {
      from: 'path/to/file.txt',
      to: 'file/without/extension',
      toType: 'file'
    },
  ], options)
]
```
### template
```
[
  new CopyWebpackPlugin([
    {
      from: 'src/',
      to: 'dest/[name].[hash].[ext]',
      toType: 'template'
    }
  ], options)
]
```

## Other Properties Of `[patterns]`
#### test

Defines a regexp to match parts of the file path
#### force
I don't know what this does and documentation doesn't state explicitly.
#### ignore
Array of globs to ignore
#### flatten
Same
#### transform
Takes in the content and the path either as a function or a promise and I'm guessing transforms it.

### Context

A path that determines how to interpret the from path, shared for all patterns

```
[
  new CopyWebpackPlugin([
    { from: 'src/*.txt', to: 'dest/', context: 'app/' }
  ], options)
]
```



toType 
