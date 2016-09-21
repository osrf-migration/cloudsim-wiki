# Server structure

1. Servers use nodejs and express. cloudsim-auth, cloudsim-sim, cloudsim-keys share a common structure (this is the structure discussed here). This shared structure should be used when developing a new server.

1. cloudsim-portal's structure is slightly different, because of its origin as a MEAN stack project.

## Directory structure

Cloudsim servers are usually contained in a Mercurial repository hosted on Bitbucket.
The root directory in the server repository should contain:

1. a .hgignore (could be .gitignore if using git) with at least the following:

        .env
        node_modules

1. A .env file: this file is not under source control, and should contain the server configuration (port number, etc) as well as any secrets (user/passwords)


