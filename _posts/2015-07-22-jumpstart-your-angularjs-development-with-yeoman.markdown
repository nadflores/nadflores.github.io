---
title:  "Jumpstart Your AngularJS Development with Yeoman"
date:   2015-07-22 9:00:00
description: A scaffolding tool for AngularJS
---

## A little background

For the past 6 months I was developing AngularJS using Apache  server and Eclipse environment. I honestly did not like it. Just for the purpose of keeping sync with the team, I had to endure the pain of re-compiling the whole assets(js and css files) just to see the change in the codebase.

But just a month ago I had a chance to lead the 2.0 version of the web app, of course using angular. I had to find a better solution for a much efficient working environment. And I found the right tool. [Yeoman!][yo]

## The Yeoman Way

According to the Yeoman site, it comprises three types of tools for improving your productivity and satisfaction when building a web app: the scaffolding tool (yo), the build tool (Grunt, Gulp, etc) and the package manager (like Bower and npm).

For this demo we will use the [generator-gulp-angular][gulp-generator].  I personally like gulp. This [post][post] is probably the reason why. 

## So let’s get started!

Install the required tools: `yo`, `gulp`, `bower`

```
npm install -g yo gulp bower
```

Install `generator-gulp-angular`:

```
npm install -g generator-gulp-angular
```

Make a new directory, and `cd` into it:

```
mkdir my-new-project && cd $_
```

Run `yo gulp-angular`, optionally passing an app name:

```
yo gulp-angular [app-name]
```

Run the app on localhost:4000

```
gulp serve
```

### Use Gulp tasks

* ```gulp``` or `gulp build` to build an optimized version of your application in `/dist`
* `gulp serve` to launch a browser sync server on your source files
* `gulp serve:dist` to launch a server on your optimized application
* `gulp test` to launch your unit tests with Karma
* `gulp test:auto` to launch your unit tests with Karma in watch mode
* `gulp protractor` to launch your e2e tests with Protractor
* `gulp protractor:dist` to launch your e2e tests with Protractor on the dist files

[yo]: http://yeoman.io/
[gulp-generator]: https://github.com/Swiip/generator-gulp-angular
[post]: https://medium.com/@preslavrachev/gulp-vs-grunt-why-one-why-the-other-f5d3b398edc4
