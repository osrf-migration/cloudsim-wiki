[Back to Home](Home)

## Configuration ##

Clients and servers can have a `.env` file for configuration. This file is not
under source control.

### Cloudsim-grant ###

No config necesary, because it's a component. 
However you can use it from the command line to generate authentication keys for the
authentication server:

    $node
    > const csgrant = require('cloudsim-grant')
    > const keys = csgrant.token.generateKeys()
    > keys
    { private: '-----BEGIN RSA PRIVATE KEY-----\nMIIBOQIBAAJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaKeD4bZ5So0RmyXSiMa/AK\nJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQUCQG3+vuMvFNaSivw9yuKVvdfm\nnWHXNXhuxpgV7HbtdBSNhF+wAAJ79iCXA82TeotISHxvDs5glrFOXJG69SQLjM0C\nIQDFM4+P44uIgaoAtWbcjAcdokC4IJ8b36yuTlBIij1RtQIhALJ9YNwJY6udsxXA\nGKceRqRgcAENewuGUmmA7E1+eIwBAiEAncLZP+k8bTSIAJEfFtZsF7UAk01MFkyK\nJQtzbTtkQV0CIQCOyrPjOrYi5I9Ema1Sfp7p5sAA15Wi0duHmlakZS08zQIgaU8T\n2vgd3YoM4k0wiCVxgIDY2qA7ZOWDFtNF8pEkQqE=\n-----END RSA PRIVATE KEY-----',
      public: '-----BEGIN PUBLIC KEY-----\nMFowDQYJKoZIhvcNAQEBBQADSQAwRgJBAIl+bpv62gw3LbtNPZs7LU3gRLpNAtaK\neD4bZ5So0RmyXSiMa/AKJ8gZ2zZ33NhoHJ47i7AS48OhC4VmSHXETbUCAQU=\n-----END PUBLIC KEY-----' }

You can then paste the keys to the .env files of your choice.

### Cloudsim-widgets ###

Cloudsim-widgets needs to know where the auth server and the portal servers are located.
If you are not working against local versions of the servers, you can use the public ones.
This is an example of the `.env` file in Cloudsim-widgets that uses the beanstalk servers:

    CLOUDSIM_AUTH_URL=https://107.22.153.254:4000
    CLOUDSIM_PORTAL_URL=https://cloudsimportal-env.us-east-1.elasticbeanstalk.com:4000

### Cloudsim-portal ###

Cloudsim-portal needs AWS access keys in order to launch machines. It also needs
Cloudsim-auth's public key to decode webtokens. See more information
here.
The `.env`file will have the following:

    CLOUDSIM_AUTH_PUB_KEY=
    AWS_SECRET_ACCESS_KEY=
    AWS_ACCESS_KEY_ID=


### Cloudsim-auth ###

Cloudsim-auth needs the following keys for webtoken decoding:

    CLOUDSIM_AUTH_PUB_KEY=
    CLOUDSIM_AUTH_PRIV_KEY=

[Proceed to Running locally](Running_locally)
