# HTML STRING REPLACE WEBPACK PLUGIN

[![npm version](https://badge.fury.io/js/html-string-replace-webpack-plugin-webpack-5.svg)](https://badge.fury.io/js/html-string-replace-webpack-plugin-webpack-5)
[![npm](https://img.shields.io/npm/dm/html-string-replace-webpack-plugin-webpack-5.svg)](https://www.npmjs.com/package/html-string-replace-webpack-plugin-webpack-5)
[![Inline docs](http://inch-ci.org/github/deviousm/html-string-replace-webpack-plugin-webpack-5.svg?branch=master)](http://inch-ci.org/github/deviousm/html-string-replace-webpack-plugin-webpack-5)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/deviousm/html-string-replace-webpack-plugin-webpack-5/issues)

This is a webpack plugin that replace string in html files that created by `html-webpack-plugin`.  
This is especially useful for adding some cdn prefix.

# Installation

#### Install the plugin with npm:

```bash
$ npm install html-string-replace-webpack-plugin-webpack-5 --save-dev
```

# Basic Usage

Add plugin to webpack config `plugins`. And pass options.

```javascript
var HtmlStringReplace = require("html-string-replace-webpack-plugin-webpack-5");
var webpackConfig = {
  entry: "index.js",
  output: {
    path: "dist",
    filename: "index_bundle.js"
  },
  plugins: [
    new HtmlWebpackPlugin(),
    new HtmlStringReplace({
      enable: true,
      patterns: [
        {
          match: /href/g,
          replacement: function(match) {
            return match;
          }
        }
      ]
    })
  ]
};
```

# Configuration

You can pass a hash of configuration options to HtmlStringReplace.  
Allowed values are as follows:

- `enable`: `true | false` whether enable this plugin or not.
- `patterns`: add some patterns and how to replace the string.
- `patterns[parrern].replacement` standard [ECMAScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace) replace function or string

example:

```javascript
new HtmlStringReplace({
  enable: true,
  patterns: [
    {
      // eg.
      // <link href="build.css">  =>
      // <link href="//cdn.baidu.com/static/build.css">
      match: /href=\"([^\"]*)\"/g,
      replacement: function(match, $1) {
        return 'href="' + CDN_PREFIX + $1 + '"';
      }
    },
    {
      // eg.
      // <script src="build.js">  =>
      // <script src="//cdn.baidu.com/static/build.js">
      match: /src=\"([^\"]*)\"/g,
      replacement: 'href="' + CDN_PREFIX + '$1"'
    }
  ]
});
```