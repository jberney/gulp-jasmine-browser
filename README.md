# gulp-jasmine-browser
[![Build Status](https://magnum.travis-ci.com/pivotal-cf/gulp-jasmine-browser.svg?token=qqbUN3LT4qYTrsZnjZQ5)](https://magnum.travis-ci.com/pivotal-cf/gulp-jasmine-browser)

## Installing
`gulp-jasmine-browser` will soon be available as an
[npm package](https://www.npmjs.com/package/gulp-jasmine-browser).
For now, npm install from github directly.

## Usage

### Create a Jasmine server to run specs in a browser

In `gulpfile.js`

```js
var gulp = require('gulp');
var jasmineBrowser = require('gulp-jasmine-browser');

gulp.task('jasmine', function() {
  return gulp.src(['src/**/*.js', 'spec/**/*.js'])
    .pipe(jasmineBrowser.specRunner())
    .pipe(jasmineBrowser.server());
});
```
In `gulp.src` include all files you need for testing other than jasmine itself.
This should include your spec files, and may also include your production JavaScript and
CSS files.

### Run jasmine tests headlessly

In `gulpfile.js`

```js
var gulp = require('gulp');
var jasmineBrowser = require('gulp-jasmine-browser');

gulp.task('jasmine-phantom', function() {
  return gulp.src(['src/**/*.js', 'spec/**/*.js'])
    .pipe(jasmineBrowser.specRunner({console: true}))
    .pipe(jasmineBrowser.phantomjs());
});
```

Note the `{console: true}` passed into specRunner.

GulpJasmineBrowser assumes that `phantomjs` is already installed and in your path.
It is only tested with PhantomJS 2.


### Usage with Webpack

If you would like to compile your front end assets with Webpack, for example to use
commonjs style require statements, you can pipe the compiled assets into
GulpJasmineBrowser.

In `gulpfile.js`

```js
var gulp = require('gulp');
var jasmineBrowser = require('gulp-jasmine-browser');
var webpack = require('gulp-webpack');

gulp.task('jasmine', function() {
  return gulp.src(['src/**/*.js', 'spec/**/*.js'])
    .pipe(webpack({watch: true, output: {filename: 'spec.js'}}))
    .pipe(jasmineBrowser.specRunner())
    .pipe(jasmineBrowser.server());
});
```

## Development
### Getting Started
The application requires the following external dependencies:
* [Node](https://nodejs.org/)
* [PhantomJS](http://phantomjs.org/) - if you want to run tests with Phantom, see your options under 'Usage.'

The rest of the dependencies are handled through:
```bash
npm install
```

Run tests with:
```bash
npm test
```

(c) Copyright 2015 Pivotal Software, Inc. All Rights Reserved.
