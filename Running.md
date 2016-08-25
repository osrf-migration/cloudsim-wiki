[Back to Home](Home)

# Running #

To have the whole Cloudsim app running, we need to launch 3 servers:

* Authentication server
* Portal
* Widgets

## Cloudsim-auth ##

The first server to be launched is `cloudsim-auth`. Both the other servers
will use it for authentication.

### Configuration ###

All servers need a `.env` file for configuration. This file is not
under source control and must be created locally. The authentication server needs
the following keys in the `.env` file for webtoken decoding:

    CLOUDSIM_AUTH_PUB_KEY=
    CLOUDSIM_AUTH_PRIV_KEY=

`cloudsim-grant` provides a convenient way to generate these keys using nodejs. You
can generate them as follows:

    node
    > const csgrant = require('cloudsim-grant')
    > const keys = csgrant.token.generateKeys()
    > keys
    { private: '-----BEGIN RSA PRIVATE KEY-----\nMIIBOQIBAAJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaKeD4bZ5So0RmyXSiMa/AK\nJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQUCQG3+vuMvFNaSivw9yuKVvdfm\nnWHXNXhuxpgV7HbtdBSNhF+wAAJ79iCXA82TeotISHxvDs5glrFOXJG69SQLjM0C\nIQDFM4+P44uIgaoAtWbcjAcdokC4IJ8b36yuTlBIij1RtQIhALJ9YNwJY6udsxXA\nGKceRqRgcAENewuGUmmA7E1+eIwBAiEAncLZP+k8bTSIAJEfFtZsF7UAk01MFkyK\nJQtzbTtkQV0CIQCOyrPjOrYi5I9Ema1Sfp7p5sAA15Wi0duHmlakZS08zQIgaU8T\n2vgd3YoM4k0wiCVxgIDY2qA7ZOWDFtNF8pEkQqE=\n-----END RSA PRIVATE KEY-----',
      public: '-----BEGIN PUBLIC KEY-----\nMFowDQYJKoZIhvcNAQEBBQADSQAwRgJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaK\neD4bZ5So0RmyXSiMa/AKJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQU=\n-----END PUBLIC KEY-----' }

You can then create the `.env` file:

    cd cloudsim-auth
    gedit .env

And in the case of the keys above, copy this into the file:

    CLOUDSIM_AUTH_PUB_KEY=-----BEGIN PUBLIC KEY-----\nMFowDQYJKoZIhvcNAQEBBQADSQAwRgJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaK\neD4bZ5So0RmyXSiMa/AKJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQU=\n-----END PUBLIC KEY-----
    CLOUDSIM_AUTH_PRIV_KEY=-----BEGIN RSA PRIVATE KEY-----\nMIIBOQIBAAJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaKeD4bZ5So0RmyXSiMa/AK\nJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQUCQG3+vuMvFNaSivw9yuKVvdfm\nnWHXNXhuxpgV7HbtdBSNhF+wAAJ79iCXA82TeotISHxvDs5glrFOXJG69SQLjM0C\nIQDFM4+P44uIgaoAtWbcjAcdokC4IJ8b36yuTlBIij1RtQIhALJ9YNwJY6udsxXA\nGKceRqRgcAENewuGUmmA7E1+eIwBAiEAncLZP+k8bTSIAJEfFtZsF7UAk01MFkyK\nJQtzbTtkQV0CIQCOyrPjOrYi5I9Ema1Sfp7p5sAA15Wi0duHmlakZS08zQIgaU8T\n2vgd3YoM4k0wiCVxgIDY2qA7ZOWDFtNF8pEkQqE=\n-----END RSA PRIVATE KEY-----

It's also possible to choose which port the server will be listening on. Let's add the
following to `.env` so the auth server is on port 8000:

    CLOUDSIM_PORT=8000

### Running ###

To run the server, simply run:

    cd cloudsim-auth
    gulp serve

By default, the server is launched on port 4000, but since we specified 8000 on
`.env`, that will be used.

To check what port is being used, search in the output of the previous
command for something like:

    listening on port 8000

Now go to your browser and open
[https://localhost:8000](https://localhost:8000)
. Accept the invalid security certificate, and your server is ready to be used.

> Note that you must accept the invalid certificates for every browser you use.

## Cloudsim-portal ##

Now we'll launch the portal server, which manages users and talks to Amazon AWS
to launch machines.

### Configuration ###

AWS keys are needed to launch machines. You can see more information
[here](https://bitbucket.org/osrf/cloudsim-portal) on how to setup AWS.

The portal also needs Cloudsim-auth's public key to decode webtokens.

TODO: does it need the auth url?

Thus, the `.env`file will have the following:

    CLOUDSIM_AUTH_PUB_KEY=
    AWS_SECRET_ACCESS_KEY=
    AWS_ACCESS_KEY_ID=

### Running ###

To run the server, simply run:

    cd cloudsim-auth
    gulp serve

By default, the server is launched on port 4000. You can check that in the
output of the command above there is something like:
TODO: How to change ports?

    listening on *:4000

Now go to your browser and open
[https://localhost:4000](https://localhost:4000)
. Accept the invalid security certificate, and your server is ready to be used.

## Cloudsim-widgets ##

The last server to launch is the one for the graphical user interface.

### Configuration ###

Cloudsim-widgets needs to know where the auth server and the portal servers are located.
If you are not working against local versions of the servers, you can use the public ones.
This is an example of the `.env` file in Cloudsim-widgets that uses the beanstalk servers:

    CLOUDSIM_AUTH_URL=https://107.22.153.254:4000
    CLOUDSIM_PORTAL_URL=https://cloudsimportal-env.us-east-1.elasticbeanstalk.com:4000

[Proceed to Running locally](Running_locally)
