[Back to Running](Running)

# Running cloudsim-portal

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
the port which is forwarded to the proxy server, usually 8081. Read more about
deployment [here](Deployment).

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

[Back to Running](Running)
