
## What
Normally, Webpack looks for **index** file when the path passed to `require` points to a directory; which means there may have a lot of **index** files.

This plugin makes it possible to use the name of the directory as the name of the entry file, makes it easier to find.

## Usage

Add the following to Webpack's config file:

```javascript
  var DirectoryNamedWebpackPlugin = require("directory-named-webpack-plugin");

  plugins: [
    new webpack.ResolverPlugin(new DirectoryNamedWebpackPlugin())
  ]

```

Then when `require("component/foo")` and the path "component/foo" is resolved to a directory, Webpack will try to look for `component/foo/foo.js` as the entry.

If there is also an index file, e.g. `index.js`, and it should be used as entry file instead of the file with the same name of directory, pass `true` as the first argument when creating new instace.

```javascript
  var DirectoryNamedWebpackPlugin = require("directory-named-webpack-plugin");

  plugins: [
    new webpack.ResolverPlugin(new DirectoryNamedWebpackPlugin(true))
  ]

```

Can also pass in an options object to further customise the plugin
``` javascript
  var DirectoryNamedWebpackPlugin = require("directory-named-webpack-plugin");

  plugins: [
    new webpack.ResolverPlugin(new DirectoryNamedWebpackPlugin({
      honorIndex: true | false, // defaults to false
      honorPackage: true | false, // defaults to true. Respect any existing
                                  // package.json's "main" property
      ignoreFn: function(webpackResolveRequest) {
        // custom logic to decide whether request should be ignored
        // return true if request should be ignored, false otherwise
        return false; // default
      }
    }))
  ]

```
