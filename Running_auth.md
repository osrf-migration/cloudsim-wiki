[Back to Running](Running)

# Running  cloudsim-auth

The first server to be launched is `cloudsim-auth`. Both the other servers
will use it for authentication.

### Configuration ###

All servers need a `.env` file for configuration. This file is not
under source control and must be created locally. To create the `.env`
file:

    cd cloudsim-auth
    gedit .env

Then add the following environment variables:

#### Admin user

You can specify the admin user, which will start with all permissions:

* `CLOUDSIM_ADMIN`

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

> **Note**: When deploying with AWS Elastic Beanstalk, `PORT` will be automatically set to
the port which is forwarded to the proxy server, usually 8081. Read more about
deployment [here](Deployment).

#### Auth0 credentials

You must provide credentials for your [Auth0](https://auth0.com/) account:

* `AUTH0_CLIENT_ID`
* `AUTH0_CLIENT_SECRET`
* `AUTH0_DOMAIN`

Clients created after 6th December 2016 no longer have their Client Secret encoded in base64. Auth0 will let you know whether the secret is encoded or not:

![Capture 2017-07-07_10-12-6_am.png](https://bitbucket.org/repo/eaE4bR/images/1833695783-Capture%202017-07-07_10-12-6_am.png)

In the `.env` file, we need to provide the **base64 encoded** secret. For example, if our secret is "v2TL3HpNwD38ryKmVW" then we need to do the following:

    echo v2TL3HpNwD38ryKmVW | base64

The result is the encoded string: "djJUTDNIcE53RDM4cnlLbVZXCg==", so in the `.env` file, we include:

    AUTH0_CLIENT_SECRET=djJUTDNIcE53RDM4cnlLbVZXCg==

Make sure you include the url of the Auth Server and the Widgets Server in your
client's allowed callbacks, and that the OAuth's JsonWebToken Signature Algorithm is HS256.

To easily get an ID token, you can install the Auth0 Authentication API Debugger extension in your client. For more details, see the [Authentication API](https://auth0.com/docs/api/authentication#login). This token is used to get a Cloudsim token.

### Running ###

To run the server, simply run:

    cd cloudsim-auth
    npm start

By default, the server is launched on port 4000, but since we specified 4001 on
`.env`, that will be used.

To check what port is being used, search in the output of the previous
command for something like:

    listening on port 4001

Now go to your browser and open
[http://localhost:4001](http://localhost:4001) to check that the server is
running.

[Back to Running](Running)