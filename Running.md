[Back to Home](Home)

# Running #

To have the whole Cloudsim app running, we need to launch 3 servers:

* Authentication server
* Portal
* Widgets

If you're planning on using the live auth and portal servers, skip to
`Cloudsim-widgets`.

## Cloudsim-auth ##

The first server to be launched is `cloudsim-auth`. Both the other servers
will use it for authentication.

### Configuration ###

All servers need a `.env` file for configuration. This file is not
under source control and must be created locally. To create the `.env`
file:

    cd cloudsim-auth
    gedit .env

Then add the following environment variables:

#### Webtoken decoding

Two keys are necessary for webtoken decoding:

* `CLOUDSIM_AUTH_PUB_KEY`
* `CLOUDSIM_AUTH_PRIV_KEY`

`cloudsim-grant` provides a convenient way to generate these keys using
nodejs. You can generate them as follows:

    node
    > const csgrant = require('cloudsim-grant')
    > const keys = csgrant.token.generateKeys()
    > keys
    { private: '-----BEGIN RSA PRIVATE KEY-----\nMIIBOQIBAAJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaKeD4bZ5So0RmyXSiMa/AK\nJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQUCQG3+vuMvFNaSivw9yuKVvdfm\nnWHXNXhuxpgV7HbtdBSNhF+wAAJ79iCXA82TeotISHxvDs5glrFOXJG69SQLjM0C\nIQDFM4+P44uIgaoAtWbcjAcdokC4IJ8b36yuTlBIij1RtQIhALJ9YNwJY6udsxXA\nGKceRqRgcAENewuGUmmA7E1+eIwBAiEAncLZP+k8bTSIAJEfFtZsF7UAk01MFkyK\nJQtzbTtkQV0CIQCOyrPjOrYi5I9Ema1Sfp7p5sAA15Wi0duHmlakZS08zQIgaU8T\n2vgd3YoM4k0wiCVxgIDY2qA7ZOWDFtNF8pEkQqE=\n-----END RSA PRIVATE KEY-----',
      public: '-----BEGIN PUBLIC KEY-----\nMFowDQYJKoZIhvcNAQEBBQADSQAwRgJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaK\neD4bZ5So0RmyXSiMa/AKJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQU=\n-----END PUBLIC KEY-----' }

In the case of the keys above, copy this into the file:

    CLOUDSIM_AUTH_PUB_KEY=-----BEGIN PUBLIC KEY-----\nMFowDQYJKoZIhvcNAQEBBQADSQAwRgJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaK\neD4bZ5So0RmyXSiMa/AKJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQU=\n-----END PUBLIC KEY-----
    CLOUDSIM_AUTH_PRIV_KEY=-----BEGIN RSA PRIVATE KEY-----\nMIIBOQIBAAJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaKeD4bZ5So0RmyXSiMa/AK\nJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQUCQG3+vuMvFNaSivw9yuKVvdfm\nnWHXNXhuxpgV7HbtdBSNhF+wAAJ79iCXA82TeotISHxvDs5glrFOXJG69SQLjM0C\nIQDFM4+P44uIgaoAtWbcjAcdokC4IJ8b36yuTlBIij1RtQIhALJ9YNwJY6udsxXA\nGKceRqRgcAENewuGUmmA7E1+eIwBAiEAncLZP+k8bTSIAJEfFtZsF7UAk01MFkyK\nJQtzbTtkQV0CIQCOyrPjOrYi5I9Ema1Sfp7p5sAA15Wi0duHmlakZS08zQIgaU8T\n2vgd3YoM4k0wiCVxgIDY2qA7ZOWDFtNF8pEkQqE=\n-----END RSA PRIVATE KEY-----

#### Custom port:

It's also possible to choose which port the server will be listening on. Let's add the
following to `.env` so the auth server is on port 4001:

    PORT=4001

> **Note**: When deploying with Elastic Beanstalk, `PORT` will be automatically set to
the port which is forwarded to the proxy server, usually 8081.

#### Auth0 credentials

You must provide credentials for your Auth0 account:

* `AUTH0_CLIENT_ID`
* `AUTH0_CLIENT_SECRET`
* `AUTH0_DOMAIN`

### Running ###

To run the server, simply run:

    cd cloudsim-auth
    gulp serve

By default, the server is launched on port 4000, but since we specified 4001 on
`.env`, that will be used.

To check what port is being used, search in the output of the previous
command for something like:

    listening on port 4001

Now go to your browser and open
[http://localhost:4001](http://localhost:4001) to check that the server is
running.

> Read about [HTTPS](HTTPS)

## Cloudsim-portal ##

Now we'll launch the portal server, which manages users and talks to Amazon AWS
to launch machines.

### Configuration ###

Create the `.env` file:

    cd cloudsim-portal
    gedit .env

Then add the following environment variables:

#### AWS keys

AWS keys are needed to launch machines. You can see more information
[here](https://bitbucket.org/osrf/cloudsim-portal) on how to setup AWS.

* `AWS_SECRET_ACCESS_KEY`
* `AWS_ACCESS_KEY_ID`

> If you use your own AWS keys, you probably won't have access to the ami's which
> are currently hardcoded in the user interface. This means that you'll need to
> [create your own amis](Developing_sim) which have `cloudsim-sim` and change the code in
> `cloudsim-widgets` to use those.

#### Cloudsim-auth's credentials

The portal also needs Cloudsim-auth's public key to decode webtokens.
If using the keys above, it would be:

    CLOUDSIM_AUTH_PUB_KEY=-----BEGIN PUBLIC KEY-----\nMFowDQYJKoZIhvcNAQEBBQADSQAwRgJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaK\neD4bZ5So0RmyXSiMa/AKJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQU=\n-----END PUBLIC KEY-----

#### Custom port:

Again, let's add a custom port to `.env`.

    PORT=4002

> **Note**: When deploying with Elastic Beanstalk, `PORT` will be automatically set to
the port which is forwarded to the proxy server, usually 8081.

#### Admin user

You can specify the admin user, which will start with all permissions:

* `CLOUDSIM_ADMIN`

### Running ###

You must start a mongodb database before running the portal. More
instructions
[here](https://bitbucket.org/osrf/cloudsim-portal).

To run the server, simply run:

    cd cloudsim-portal
    gulp serve

By default, the server is launched on port 4000, but since we specified 4002 on
`.env`, that will be used.

To check what port is being used, search in the output of the previous
command for something like:

    listening on port 4002

Now go to your browser and open
[http://localhost:4002](http://localhost:4002) and check that the server is
running.

> Read about [HTTPS](HTTPS)

## Cloudsim-widgets ##

The last server to launch is the one for the graphical user interface. It will
communicate with both the auth and portal servers.

### Configuration ###

Create the `.env` file:

    cd cloudsim-widgets
    gedit .env

Then add the following environment variables:

#### Server URLs

Cloudsim-widgets needs to know where the auth server and the portal servers are
located. To use the previously launched servers, the `.env` file will look like
this:

    CLOUDSIM_AUTH_URL=http://localhost:4001
    CLOUDSIM_PORTAL_URL=http://localhost:4002

If you are not working against local versions of the servers, you can use the public ones.
This is an example of the `.env` file in Cloudsim-widgets that uses the beanstalk servers:

    CLOUDSIM_AUTH_URL=https://devauth.cloudsim.io
    CLOUDSIM_PORTAL_URL=https://devportal.cloudsim.io

#### Auth0 credentials

You must provide credentials for your Auth0 account:

* `AUTH0_CLIENT_ID`
* `AUTH0_DOMAIN`

#### Users

You can specify the admin user, and for debugging, also some other users:

* `CLOUDSIM_ADMIN`
* `SRC_ADMIN`
* `SRC_COMPETITOR`
* `ARIAC_ADMIN`
* `ARIAC_COMPETITOR`

### Running ###

To run the server, simply run:

    cd cloudsim-widgets
    gulp serve

By default, the server is launched on port 5000.

To check what port is being used, search in the output of the previous
command for something like:

           Local: https://localhost:5000

Now go to your browser and open
[https://localhost:5000](https://localhost:5000)
. Accept the invalid security certificate, and the Cloudsim website will appear!

## Checking if everything is working ##

You can do a simple check as follows:

1. Enter [https://localhost:5000/](https://localhost:5000/)

1. Create an account with the admin's username.

1. Use the password to login

1. You should now be inside the dashboard, this means we're successfully talking
to the `cloudsim-auth` server!

1. You should see a `Launch a machine` widget. If you don't, either we're not
talking to the server, or there's an issue with the admin name.

1. Click on the `Launch!` button, and a new machine should appear, this means
we're successfully talking to the `cloudsim-portal` server and the portal is
successfully talking to AWS!

