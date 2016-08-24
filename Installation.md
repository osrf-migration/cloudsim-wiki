[Back to Home](Home)

## Install dependencies ##

1. Install basic tools

        sudo apt get install -y curl mercurial git python-pip

1. Install **vcs**, a tool to manage multiple repositories

        sudo apt-get install python-vcstool

1. Install **nodejs** (must be version 4 and up)

        curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
        sudo apt install -y nodejs

1. Install global node modules:

    a. Bower, the package manager for the browser components

       npm install -g bower

    b. Gulp, the web "make"

       npm install -g gulp

    c. Polymer

       npm install -g polymer-cli

> Note: when installing npm modules, you shouldn't have to be the root user.
> Npm installs packages locally (in the node_modules directory located besides
> the package.json file). However when you install global packages (with npm -g),
> it can happen that npm fails because it wants to write in /usr/bin or somewhere.
> For those cases, you should use sudo.


## Get and link cloudsim source code ##

1. Clone the master CloudSim repository:

        hg clone http://bitbucket.org/osrf/cloudsim
        cd cloudsim

1. Run [build.bash](https://bitbucket.org/osrf/cloudsim/src/default/build.bash)
to get the sources and create links accross projects.

        bash build.bash

    `build.bash` does many things, and each of them could fail.

    1. The vcs import command clones all the repos, so **make sure you have ssh setup
    with bitbucket and github**.

### Projects and links explained ###

Cloudsim uses 2 javascript package managers: `npm` for server side components and
servers, and `bower` for client side web components.

Packages can either be installed or linked:

1. Installled packages are downloaded and installed from versioned tar balls,
and are useful for production.

1. Linked packages allow you to use local copies of repositories, and are
useful for development.

The `build.bash` script links the cloudsim packages:

1. `bower_create_links` and `npm_create_links` make local copies available to
be used by others.
1. `bower_use_links` and `npm_use_links` create the symlinks.

[Proceed to Configuration](Configuration)