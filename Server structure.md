# Server structure

Servers use nodejs and express. cloudsim-auth, cloudsim-sim, cloudsim-keys share a common structure (this is the structure discussed here). This shared structure should be used when developing a new server.
Unlike normal web servers that typically serve web pages, cloudsim servers only serve json data. A typical cloudsim web app connects to many servers simultaneously.

1. cloudsim-portal's structure is slightly different, because of its origin as a MEAN stack project. Therefore, its structure should not be used as a template.

1. 

## Directory structure

Cloudsim servers are usually contained in a Mercurial repository hosted on Bitbucket.
The root directory in the server repository should contain:

1. A README.md file: this file contains a high level description and general build instructions.

1. A .hgignore (could be .gitignore if using git) with at least the following:

        .env
        node_modules

1. A .env file: this file is not under source control, and should contain the server configuration (port number, etc) as well as any secrets (user/passwords)

1. A package.json file: this file contains the npm scripts (start, test), dependencies (nmp packages). We try to use the `devDependencies` to distinguish between modules that are used for testing and development as opposed to production. 

1. A `server` directory: this directory contains the files that run on the server (as opposed to the browser)

1. A `test` directory: this directory contains the unit tests.

## server file structure

The server should be contained in a single js file, named after the project. This is preferred to `server.js`, because it is easier to distinguish servers when running multiple servers on a single machine.

The server should use the following modules and practices:


The first task of the server is to `require` other modules (using  a const declaration). Typically, this consist of:

* morgan (to log requests)
* bodyParser (to generate the `req.body` data)
* express (to create the app, and routing / middle ware patterns)
* dotenv (to load the content of the `.env` file into the `process.env` object)
* cloudsim-grant (to access the db, verify tokens)
* each collection should also be required (using the relative path, usually `.`)

The server should have a `test` mode:

* use `process.env.NODE_ENV` to look for "test"
* name the database collection accordingly (usually add a '-test' to the name)

The server should then:

* look for an initial user in `process.env.ADMIN_USER`
* define the initial resources and their data
* call cloudsim-grant.init

The server file should then:

* setup global routes ( like "/", "/permissions")
* call the setRoutes for each collections


Finally, the server should listen for traffic on port `process.env.PORT`


## Collections

Collections are data types (usually in a list form) that is served by a server. Typical collections for cloudsim are:

* simulator machines
* simulation tasks
* groups of users

1. Each collection is contained in a single js module inside the server module.

* The module is named after the collection `simulators.js`
* The name of the routes should be the same as the name of the collection `/simulators`
* If you need to split a collection into multiple files, put them in a directory 
named after the collction/route `simulators`
* The module exports a `setRoute` function.


1. Each collection unit tests are contained in a single js module in the test directory. Tests can be:

* internal testing of exported module code
* calls to middleware with mock requests and responses
* call to the entire running server, using supertest.

## build tools, best practices

While certain servers use `gulp` as a build tool, this practice is discouraged (now) in favor of using scripts defined in package.json.

You are encouraged to use the new features of the javascript language:

* `const` and `let` over `var`
*  classes
*  avoid unnecessary semi colons `;`
*  es6 strings templates (they are multiline strings, like Python's """ strings)
*  arrow functions for cases where `this` is not used: (x,y) => x + y

