# Server structure

Servers use nodejs and express. cloudsim-auth, cloudsim-sim, cloudsim-keys share a common structure (this is the structure discussed here). This shared structure should be used when developing a new server.
Unlike normal web servers that typically serve web pages, cloudsim servers only serve json data. A typical cloudsim web app connects to many servers simultaneously.

1. cloudsim-portal's structure is slightly different, because of its origin as a MEAN stack project.

## Directory structure

Cloudsim servers are usually contained in a Mercurial repository hosted on Bitbucket.
The root directory in the server repository should contain:

1. A README.md file: this file contains a high level description and general build instructions.

1. A .hgignore (could be .gitignore if using git) with at least the following:

        .env
        node_modules

1. A .env file: this file is not under source control, and should contain the server configuration (port number, etc) as well as any secrets (user/passwords)

1. A package.json file: this file contains the npm scripts (start, test), dependencies (nmp packages).

1. A `server` directory: this directory contains the files that run on the server (as opposed to the browser)

1. A `test` directory: this directory contains the unit tests.


## Collections
 


