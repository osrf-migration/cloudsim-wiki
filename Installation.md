[Back to Home](Home)

## Install dependencies ##

1. Install basic tools

        sudo apt-get install -y curl mercurial git python-pip redis-server

1. Install **vcs**, a tool to manage multiple repositories 
> Note: this may fail if you haven't installed ROS yet. Check https://github.com/dirk-thomas/vcstool#how-to-install-vcstool (or install ROS :)).

        sudo apt-get install python-vcstool

1. Install **nodejs** (must be version 4 and up)

        curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
        sudo apt-get install nodejs 

1. Install global node modules:

    a. Bower, the package manager for the browser components

           sudo npm install -g bower

    b. Gulp, the web "make"

           sudo npm install -g gulp

    c. Polymer

           sudo npm install -g polymer-cli

> Note: when installing npm modules, you shouldn't have to be the root user.
> Npm installs packages locally (in the node_modules directory located besides
> the package.json file). However when you install global packages (with npm -g),
> it can happen that npm fails because it wants to write in /usr/bin or somewhere.
> For those cases, you should use sudo.


## Get and link cloudsim source code ##

1. Clone the master CloudSim repository:

        hg clone http://bitbucket.org/osrf/cloudsim
        cd cloudsim

1. Run [setup.bash](https://bitbucket.org/osrf/cloudsim/src/default/setup.bash)
to get the sources and create links across projects.

        ./setup.bash

    `setup.bash` does many things, and each of them could fail.

    1. The vcs import command clones all the repos, so **make sure you have ssh setup
    with bitbucket and github**.
    1. The `build.bash` script goes into each project and invokes `npm install` and `bower install`

Note that it is not required run `link.bash` manually if after running `setup.bash` you get the `Not linking repositories, you can run [link.bash] manually.` message. That is an optional step that you should perform only if you know what you are doing.


### Projects and links explained ###

**Important:** the description below is mainly for information purposes and should be only required under very specific development circumsatances.

Cloudsim uses 2 javascript package managers: `npm` for server side components and
servers, and `bower` for client side web components.

Packages can either be installed or linked:

1. Installed packages are downloaded and installed from versioned tar balls,
and are useful for production.

1. Linked packages allow you to use local copies of repositories, and are
useful for development.

The `link.bash` script* links the cloudsim packages:

1. `bower_create_links` and `npm_create_links` make local copies available to
be used by others.
1. `bower_use_links` and `npm_use_links` create the symlinks.

Use `clean.bash` and `build.bash` to remove links and install the software. You can then use `link.bash` to add links if you want to edit code.

\* **We don't recommend the use of `link.bash`**, since most of the time different servers need different dependencies. The recommended approach is to manually link the packages you are currently working on (e.g. if you need to work on cloudsim-grant, run `npm link cloudsim-grant`). 


[Proceed to Running](Running)