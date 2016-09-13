[Back to Running](Running)

# Running cloudsim-widgets

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

#### Custom port:

It's also possible to choose which port the server will be listening on. Let's add the
following to `.env` so the auth server is on port 5000:

    PORT=5000

> **Note**: When deploying with Elastic Beanstalk, `PORT` will be automatically set to
the port which is forwarded to the proxy server, usually 8081. Read more about
deployment [here](Deployment).

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

[Back to Running](Running)