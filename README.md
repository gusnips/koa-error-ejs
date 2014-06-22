# koa-error-ejs
  
  Error response middleware for koa supporting:
  
- text  
- html  
- json  
  
  Adapted from [koa-error](https://github.com/koajs/error) to use EJS as view engine  
  
## Installation
  
```js
$ npm install koa-error-ejs --save
```
  
  and then copy the default error view to your views folder
  
```js
$ cp node_modules/koa-error-ejs/error.html views/
```
  
  setup in your application
  
```js
var app= require('koa')();
var error= require('koa-error-ejs');
app.use(error());
```

## Options

 - `view` String path to template written with [ejs](http://embeddedjs.com). Defaults to {view.root}/error  
 - `layout` String|Boolean layout to use on error view, or false if none. Defaults to false.  
 - `custom` Object specific view for a status code, for example:  {404: 'error/not-found'}. Defaults to {}  

  Example: 
  
```js
var app= require('koa')();
var error= require('koa-error-ejs');
app.use(error({
  view: 'error/error', //(optional)
  layout: 'layouts/error', //(optional)
  custom: { //(optional)
    401: 'error/login',
    403: 'error/forbidden',
    404: 'error/not-found',
    500: 'error/sorry'
  }
}));
```

## Custom templates

  By using the `view` option you can override the bland default template,
  with the following available local variables:

  - `env`
  - `ctx`
  - `request`
  - `response`
  - `error`
  - `stack`
  - `status`
  - `code`

Here's an example:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Error - <%=status%></title>
  </head>
  <body>
    <div id="error">
      <h1>Error</h1>
      <p>Looks like something broke!</p>
      <% if(env === 'development'){ %>
      <pre>
        <code>
	  <%-stack%>
        </code>
      </pre>
      <% } %>
    </div>
  </body>
</html>
```

## License

  MIT
