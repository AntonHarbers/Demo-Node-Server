# The Odin Project - Basic Informational Site

A simple multi page informational site built using node js, html and javascript for the odin Project.

```
    The 'express' branch showcases the same project written using the express application.

    In order to run the express app, clone the express branch, install all node dependencies and run:

    npm run start

    In your console.

```

[Live Link](https://odin-node-site.tmonee23.repl.co/)

![Landing Page](/repoImages/landingPage.png)
![Contact Me](/repoImages/contactMe.png)
![About](/repoImages/about.png)
![Error](/repoImages/error.png)

## Manual

If you clone this repo and want to try it out just make sure you have the correct node version installed and run the following command in your terminal from the root directory of this project.

CMD:

```
    node index.js
```

## Folder Structure

```
    /.git               -> This git repository
    /repoImages         -> Contains the images shown in this repo
    404.html            -> Error Page
    about.html          -> About Page
    contact-me.html     -> Contact Page
    index.html          -> Landing Page
    index.js            -> Server File
    README.md           -> This Readme
```

## Key Concepts

### Node Server

This project was all about setting up a basic node server to serve html files to the client based on the given url path. This was acheived using nodejs and the HTTP and FS APIs (more on this below).

To set up node JS follow the instructions on their page: [Getting Started NodeJS](https://nodejs.org/en/learn/getting-started/how-to-install-nodejs)

### HTTP and URL APIs

I used the HTTP and URL APIs to create a server on port 8080 that takes requests and gives responses based on the path provided in our url:

JS:

```
var http = require('http');
var url = require('url');

http
  .createServer(function (req, res) {
    var q = url.parse(req.url, true);
    var filename = '.' + q.pathname;

    switch (filename) {
      case './':
        filename = 'index.html';
        break;
      case './about':
        filename = 'about.html';
        break;
      case './contact-me':
        filename = 'contact-me.html';
        break;
      default:
        filename = '404.html';
        break;
    }

})
.listen(8080);

```

### FS API

The FS API can then be used to return a response with a header and content (if there is not an error trying to read the file with the filename provided from the url and http APIs).

JS:

```
    var fs = require('fs'); // IMPORT HERE

    // ADD this to the inside of your .createServer function above to give a response to the client
    fs.readFile(filename, function (err, data) {
      if (err) {
        res.writeHead(500, { 'Content-Type': 'text/plain' });
        res.end('500 - Internal Server Error');
      } else {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.write(data);
        return res.end();
      }
    });
```

## Final Notes

A great first look at how to serve html documents to a client through a http server. NodeJs gives you great APIs and a runtime that makes all this super easy. It's a little verbose to do it this way in a time of modern frameworks, however I think its a great entry point and good foundational knowledge to help understand what these modern tools do behind the scenes.
