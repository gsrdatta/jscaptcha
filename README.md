# jscaptcha
Creates Captcha in base64 format

# installation
`npm install jscaptcha`

## API

#### `captcha(options)`  
If no option is passed, you will get a random string of six characters and corresponding svg.  
  
* `height`: 100 // height of image
* `width`: 180 // height of image (size*30)
* `size`: 6 // size of random string  
* `ignoreChars`: '0o1i' // filter out some characters like 0o1i  
* `noise`: 10 // number of noise circles  min-10,max-25
* `color`: true // characters will have distinct colors instead of grey, true if background option is set  
* `background`: '#cc9966' // background color of the svg image  

This function returns an object that has the following property:
* `data`: string // svg path data
* `text`: string // captcha text


# usage
```javascript 
// import library
var captcha = require("jscaptcha");

// Create new Captcha
var newCaptcha = captcha(options);

// Value of the captcha
var value = newCaptcha.value

// Image in base64 
var imagebase64 = newCaptcha.image;

// Width of the image
var width = newCaptcha.width;

// Height of the image
var height = newCaptcha.heigth;

```
### parameters
``` json

```

### sample usage with nodejs http
``` javascript

"use strict";
var http = require("http");
var captcha = require("nodejs-captcha");
var PORT = 8181;

function handleRequest(req, res) {
  if (req.method === "GET" && (req.url === '/' || req.url.indexOf("index") > -1)){
    let result = captcha();
    let source = result.image;
    res.end(
      `
    <!doctype html>
    <html>
        <head>
            <title>Test Captcha</title>
        </head>
        <body>
        <label>Test image</label>
        <img src="${source}" />
        </body>
    </html>
    `
    );
  }else{
      res.end('');
  }
}

//Create a server
var server = http.createServer({}, handleRequest);

//Start server
server.listen(PORT, function() {
  console.log("Server listening on: https://localhost:" + PORT);
});
```

It is recommended to store the value of the captcha in order to check the validity of the user's answer to challange
