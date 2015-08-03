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

For this demo we will use the [generator-gulp-webapp][gulp-webapp].  I personally like gulp. This [post][post] is probably the reason why. 

## So let’s get started!

Install the required tools: `yo`, `gulp`, `bower`

```
npm install -g yo gulp bower
```

Install `generator-gulp-webapp`:

```
npm install -g generator-gulp-webapp
```

Make a new directory, and `cd` into it:

```
mkdir my-new-project && cd $_
```

Run `yo gulp-webapp`, optionally passing an app name:

```
yo gulp-webapp [app-name]
```

You will be prompted to choose some premade libraries. Use `up/down` keys or `j/k` if you're familiar with vim and `space` to toggle select.
![gulp webapp](/assets/images/yo.png)

We'll cancel the `bower install && npm install` setup(`ctrl-c`), since we will include angular and bootstrap in the `bower.json` file. We'll leave the package.json as it is.

In your `bower.json` file, edit it with:

``` json
{
  "name": "my-new-project",
  "private": true,
  "dependencies": {
    "bootstrap"     : "3.3.5",
    "angular"       : "1.4.3",
    "angular-route" : "1.4.3"
  }
}
```

Then run `bower install`. This will download angular and bootstrap and will be found in `/bower_components` folder.

Let's edit and include the angular and bootstrap to your `app/index.html` file. You can copy/paste the code below.

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>my new project</title>

    <link rel="apple-touch-icon" href="apple-touch-icon.png">
    <!-- Place favicon.ico in the root directory -->

    <!-- build:css styles/vendor.css -->
    <link rel="stylesheet" href="/bower_components/bootstrap/dist/css/bootstrap.css">
    <!-- endbuild -->

    <!-- build:js scripts/vendor.js -->
    <script src="/bower_components/jquery/dist/jquery.js"></script>
    <script src="/bower_components//angular/angular.js"></script>
    <script src="/bower_components//angular-route/angular-route.js"></script>
    <!-- endbuild -->
  </head>
  <body>
    <div class="container">
      <div class="header">
        <ul class="nav nav-pills pull-right">
          <li class="active"><a href="#/">Home</a></li>
          <li><a href="#/about">About</a></li>
          <li><a href="#/contact">Contact</a></li>
        </ul>
        <h3 class="text-muted">my new project</h3>
      </div>

      <!-- ngRoute will render template here -->
      <ng-view></ng-view>

      <div class="footer">
        <p>♥ from the Yeoman team</p>
      </div>
    </div>
    
  </body>
</html>
```

## Home Page
Create the following files and code below.

`app/app.js`

```javascript
'use strict';

angular
  .module('myApp', ['ngRoute'])
  .config([ '$routeProvider', function ($routeProvider) {
    $routeProvider
      .when('/', {
        templateUrl: 'template/home.html',
        controller: 'HomeCtrl',
      })
      .otherwise({
        redirectTo: '/'
      });
  }])
```

`app/scripts/home.controller.js`

```javascript
'use strict';

angular.module('myApp')
  .controller('HomeCtrl', HomeCtrl)

HomeCtrl.$inject = ['$log', '$scope'];

function HomeCtrl($log, $scope){
  $log.debug('*********HomeCtrl*********');
}
```

`app/template/home.html`

``` html
<div class="jumbotron">
  <h1>'Allo, 'Allo!</h1>
  <p class="lead">Always a pleasure scaffolding your apps.</p>
  <p><a class="btn btn-lg btn-success" href="#">Splendid!</a></p>
</div>

<div class="row marketing">
  <div class="col-lg-6">
    <h4>HTML5 Boilerplate</h4>
    <p>HTML5 Boilerplate is a professional front-end template for building fast, robust, and adaptable web apps or sites.</p>

    <h4>Bootstrap</h4>
    <p>Sleek, intuitive, and powerful mobile first front-end framework for faster and easier web development.</p>
  </div>
</div>
```

Let's include the newly created js files to `app/index.html`.

```html
<head>
  <!-- build:js scripts/vendor.js -->
  <script src="/bower_components/jquery/dist/jquery.js"></script>
  <script src="/bower_components/angular/angular.js"></script>
  <script src="/bower_components/angular-route/angular-route.js"></script>
  <script src="app.js"></script>
  <script src="scripts/home.controller.js"></script>
  <!-- endbuild -->
</head>
```

Initialize the application using `ng-app` directive. From the `app/index.html` file.

```html
<html ng-app="myApp">
```

Run the app on `localhost:9000`

```
gulp serve
```

![yo](/assets/images/yo2.png)

## Contact and About Page

`app/scripts/contact.controller.js`

```javascript
'use strict';

angular.module('myApp')
  .controller('ContactCtrl', ContactCtrl)

ContactCtrl.$inject = ['$log', '$scope'];

function ContactCtrl($log, $scope){
  $log.debug('*********ContactCtrl*********');
}
```

`app/template/contact.html`

```html
<h2>Contact Page</h2>
```

`app/scripts/about.controller.js`

```javascript
'use strict';

angular.module('myApp')
  .controller('AboutCtrl', AboutCtrl)

AboutCtrl.$inject = ['$log', '$scope'];

function AboutCtrl($log, $scope){
  $log.debug('*********AboutCtrl*********');
}
```

`app/template/about.html`

```html
<h2>About Page</h2>
```

Let's include the newly created controllers to `app/index.html`

```html
<head>
  <!-- build:js scripts/vendor.js -->
  <script src="/bower_components/jquery/dist/jquery.js"></script>
  <script src="/bower_components/angular/angular.js"></script>
  <script src="/bower_components/angular-route/angular-route.js"></script>
  <script src="app.js"></script>
  <script src="scripts/home.controller.js"></script>
  <script src="scripts/contact.controller.js"></script>
  <script src="scripts/about.controller.js"></script>
  <!-- endbuild -->
</head>
```

## You can clone the [final app][repo]. Make sure to run `bower install && npm install`.

[yo]: http://yeoman.io/
[gulp-webapp]: https://github.com/yeoman/generator-gulp-webapp
[post]: https://medium.com/@preslavrachev/gulp-vs-grunt-why-one-why-the-other-f5d3b398edc4
[repo]: https://github.com/nadflores/yo-gulp-webapp
