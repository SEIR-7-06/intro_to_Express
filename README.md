# Intro to Express

## Lesson Objectives

1. Describe what a web server is
1. Install Node packages
1. Set up a basic Express server
1. Set up a basic GET route
1. Use nodemon to restart your sever when your code changes
1. Save a record of what packages your application uses

## Describe what a web server is

A server is just a computer that is always on and connected to the internet.  Other computers can try to connect to it to retrieve information

![Request Response Cycle](https://cdn.zapier.com/storage/photos/9ec65c79de8ae54080c1b417540469a6.png)

A web server is just a server that sends dynamic HTML pages, meaning that the HTML is pretty much the same for every page, but is altered slightly depending on the data that is requested.  Think of amazon.com where one book's page looks pretty similar to another book's page, just with different text.

In this unit, we'll be writing web applications that a computer will run that will allow the computer to respond to other computers that try to connect to it.  We'll write this code in JavaScript using Node.js, which allows us to write computer applications using JavaScript.

## What does it mean to program a server?

We need to write the code that handles requests and figures out how to respond. It might need to format data into JSON, it might need to talk to a database to request a specific resource, and it might need to check if a user is authorized to see the resource they have requested.

To write server side code, is to lay out all of the possible requests that might come in and give instructions for how to handle each type of request.

![request](https://i.imgur.com/YXgj8.png)


![image](https://cloud.githubusercontent.com/assets/6520345/18041555/0345ba10-6d6f-11e6-9a6f-c008aac1935a.png)

### What is Node?

![image](https://cloud.githubusercontent.com/assets/6520345/18023104/d38c2168-6ba9-11e6-997c-24b3a2652991.png)

![image](https://cloud.githubusercontent.com/assets/6520345/18023096/c368ce26-6ba9-11e6-805a-4562a8853721.png)

V8, the JavaScript engine that runs Chrome, is a piece of code written in C++. It creates a processor to take in JS code and translate it to make actionable assembly code/machine code so that the CPU can “do” what you have asked it to in JavaScript. Node is a program that has all of the V8 code and more. It extends V8; V8 is embedded in NodeJS, and Node adds more functionality and syntax that V8 wouldn’t be able to understand. This syntax allows you to write server-side code. (V8 is created to meet the EcmaScript 6 - the standard that defines JavaScript).

- Node.js provides the ability to handle requests and issue responses.
- It is fast.
- It is fast largely because it is asynchronous, meaning code can run in parallel without "blocking" the call stack (the list of other concurrent commands).
- Node really shines when it comes to heavy input-output type operations.
- Realtime services like chat applications or conferencing platforms benefit from using Node.
- APIs are also input/output heavy, and they also tend to work with JavaScript out of the box (think JSON). What better platform than Node?
- Node is designed to accommodate [the module pattern](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript), which means that it allows developers to write useful functionality and then share it with other developers. It is easy to pull in useful modules into your project (like express). This keeps functionality separate and helps projects feel organized.

### NPM and NPM Init
- Node Package Manager, usually called NPM, is a tool that allows us to easily download community-built Node packages.
  * For example, instead of using a CDN to download bootstrap and make sure your version is up-to-date, you can install it with NPM, which will help you manage the downloads and versions.
- Initialize new Node project with NPM: `npm init`. This will simply create one file, `package.json`.
- NPM works with `package.json`, a file in your project, which is a list of project information. NPM makes sure that packages do not get uploaded or tracked in git (imagine how much unnecessary code you could be pushing and pulling each time). To make sure all collaborators are still on the same page, any package listed in `package.json` can easily be downloaded with one command, `npm install`, when somebody clones your project.
- To install NPM packages *and* save them to `package.json`, use the `--save specification`: `npm install --save express` or `npm install --save bootstrap`.



### Express JS
Express is a cutting-edge, unopinionated, server-side JavaScript framework that runs on a Node.js server. It is a popular framework with a bevy of modules you can add to it. Node is the platform and Express provides the specific functionality. If you were building a house rather than a server, Node would be the foundation and utilities, express would be the building material that comprises the above ground building.

![image](https://cloud.githubusercontent.com/assets/6520345/18060592/f5954682-6dd3-11e6-99ba-5dc0b42a4ff8.png)




- Express is a framework built on top of Node.js that makes development of web servers more intuitive and quicker.
- Express allows us to easily set up routes that will trigger actions such as rendering pages or returning JSON.

Much like jQuery does for JavaScript, Express provides easy, intuitive syntax and a lot of built in functionality.

### Hello World in Express

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello World!'))

const server = app.listen(3000);
```




### Express file tree

With frontend and backend code to organize, we should make sure to keep our files in a logical order.

```
├── server.js  // your server code
├── package.json    // lists dependencies; changed by npm install --save somePackage
├── public  // i.e. client-side
│   ├── images  // images to serve to client
│   ├── scripts
│       └── app.js   // client-side javascript file
│   └── styles
│       └── style.css
├── vendor // optional 2nd public dir for jQuery & bootstrap if we choose not to use CDNs
├── views  // html files that we'll serve
│   └── index.html
└── node_modules  // don't edit files in here!
    ├── express // etc
```

> We should also add `node_modules` to a `.gitignore` file so it is not checked into git.  Future developers can just run `npm install` to get the packages listed in `package.json`

## Install Node packages

- People will write code and make it available online for others to use
- You use these published chunks of code to build applications faster

These chunks of code fall into one of two categories

- Libraries
    - A collection of functions, objects, and even other libraries that you call
    - It has no idea what you're going to build
- Frameworks
    - Is essentially just a library
    - Is also a pre-conceived skeleton for an application
    - It knows what you're going to build and is somewhat opinionated about how you should do it

- The libraries and frameworks that people write for Node are called "packages" and are published on [npmjs.com](https://www.npmjs.com/)
- NPM (Node Package Manager) is a command line tool that we'll use to install node packages
    - in old days we used to have to find the code's website online, then download the code

To install (download) a package, first you must know its name (each name is unique in npm).  Then run:

```
npm install package-name
```

let's install the library `express`:

```
npm install express
```

Express.js is a framework that makes it easier to build web-applications

## Set up a basic Express server

Now that the library has been installed (downloaded), we can use it in our code, by using the `require()` function

```javascript
const express = require('express');
```

- The `require()` function takes whatever code was written for the specified library and returns it
    - We'll typically store the return value of `require()` in a variable of the same name
        - Think of the variable as the library itself
- By reading [the documentation](https://www.npmjs.com/package/express), we can figure out how to use what is returned by  `require('express')`

1. Install it: `npm install express`
1. Create a file called server.js
1. Inside server.js, write the following

    ```javascript
    const express = require('express'); //from documentation: express is function
    const app = express();//app is an object

    app.listen(3000, ()=>{
        console.log("I am listening");
    });
    ```

1. Start the app by executing `node server.js` in the command line
1. Visit http://localhost:3000/ in your browser.  You've successfully created a basic web server!  This will serve dynamic pages to web browsers.

## Set up a basic GET route

Now we'll create a basic GET route so that visitors to (clients of) our web-server can retrieve some information from it

```javascript
const express = require('express'); //from documentation: express is function
const app = express();//app is an object

app.get('/somedata', (request, response) => {
    response.send('here is your information');
});

app.listen(3000, () => {
    console.log("I am listening");
});
```

- The function passed as a second parameter to `app.get()` is executed each time a user (client) goes to http://localhost:3000/somedata
- The function (callback) takes two parameters
    - `request`
        - object containing information about the request made (browser, ip, query params, etc)
    - `response`
        - object containing methods for sending information back to the user (client)

## Use nodemon to restart your sever when your code changes

An NPM package called `nodemon` allows us to run code just like `node`, but it will restart the application whenever code in the application's directory is changed.

1. Install it `npm install nodemon -g`
    - the `-g` tells npm to make the package available for use in the terminal in any directory (globally)
1. Now we can call `nodemon server.js`, and the server will restart whenever the app's code changes

## Save a record of what packages your application uses

- In general, we don't want to store our package code in our repositories, because it increases the size of the repo unnecessarily
- We can install our packages like normal but keep track of what packages were installed in a `package.json` file.
    - Then when other users download our code
        1. They simply call `npm install`
        1. NPM will then look in the package.json file to see what packages need to be installed and install them without requiring the user to type `npm install some-package` for each package the app depends on (dependency)

1. In the terminal, type: `npm init`
1. Keep hitting enter, until the program finishes
    - you should now have a package.json file
1. Install a package with `npm install some-package --save`
    - The `--save` tells npm to keep a record inside `pacakge.json` that the application depends on the package installed

Let's test this out:

1. `rm -r node_modules`
1. `npm init`
1. `npm install express --save`
1. `rm -r node_modules`
    - simulates another developer downloading your code
1. `npm install`
1. Look inside the `node_mdules` directory to see if `express` was installed

In general, we can tell git to ignore `node_modules` directories so that they don't get added accidentally

1. Create a file called `.gitignore`
1. In it, add the line `node_modules`

We can also edit package.json so that we don't need specify the script that we're going to run.  Do one of the following:

- After doing `npm init`
    - when it says `entry point: (index.js)`, specify which file you want to use (e.g. server.js)
- Edit package.json
    - where it says `"main": "index.js",` change the file name (e.g. server.js)

Now we can simply run `nodemon` without specifying the file name
