---
layout: post
title: "webpack-merge is a thing and it is beautiful"
author: nedschwartz
date: 2017-02-24T20:02:28+00:00
---

Let's say you want to redefine a loader from your base webpack config in your production webpack config. Try `webpack-merge.smart` !

## webpack.base.config.js
```javascript
const config = {
  entry: "./index.js",
  module: {
    rules: [
      {
        test: /\.css?$/,
        exclude: /node_modules/,
        use: [{
          loader: "css-loader",
          options: { sourceMap: true }, // set to true
        }],
      },
      {
        test: /\.css?$/,
        include: /node_modules/,
        use: ["css-loader"],
      },
    ],
  },
};
```

## webpack.production.config.js
```javascript
const merge = require("webpack-merge");
const baseConfig = require("webpack.base.config");

const productionConfig = {
  module: {
    rules: [{
      test: /\.css?$/,
      exclude: /node_modules/,
      use: [{
        loader: "css-loader",
        options: { sourceMap: false }, // override to false
      }],
    }],
  },
};

module.exports = merge.smart(baseConfig, productionConfig);
```

## Result
```javascript
const config = {
  entry: "./index.js",
  module: {
    rules: [
      {
        test: /\.css?$/,
        exclude: /node_modules/,
        use: [{
          loader: "css-loader",
          options: { sourceMap: false }, // yep! it's false
        }],
      },
      {
        test: /\.css?$/, // but we didn't touch this rule
        include: /node_modules/,
        use: ["css-loader"],
      },
    ], // and we didn't append anything either!
  },
};
```

`webpack-merge.smart` is aware of the shape of a webpack configuration and allows you to update only the rule you want.

Check it out: https://github.com/survivejs/webpack-merge#smart-merging
