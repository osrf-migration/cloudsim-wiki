[Back to Running](Running)

# Running cloudsim-widgets

The last server to launch is the one for the graphical user interface. It will
communicate with both the auth and portal servers.

### Configuration ###

Create the `.env` file:

    cd cloudsim-widgets
    gedit .env

Then add the following environment variables:

#### Server URLs

Cloudsim-widgets needs to know where the auth server and the portal servers are
located. To use the previously locally launched servers, the `.env` file will
look like this:

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

#### Cloudsim-auth public key

We also need the cloudsim-auth public key to use cloudsim-grant in the back end:

* `CLOUDSIM_AUTH_PUB_KEY`

#### Admin user:

* `CLOUDSIM_ADMIN`

### Running ###

To run the server in dev mode:

    cd cloudsim-widgets
    npm run dev

For production:

    npm start

To check what port is being used, search in the output of the previous
command for something like:

           Local: http://localhost:5000

Now go to your browser and open
[http://localhost:5000](http://localhost:5000) to see the app.

## Checking if everything is working ##

You can do a simple check as follows:

1. Enter [http://localhost:5000/](http://localhost:5000/)

1. Create an account with the username in `CLOUDSIM_ADMIN`.

1. Use the password to login

1. You should now be inside the dashboard, this means we're successfully talking
to the `cloudsim-auth` server!

1. You should see a `Launch a machine` widget. If you don't, either we're not
talking to the server, or there's an issue with the admin name.

1. Click on the `Launch!` button, and a new machine should appear, this means
we're successfully talking to the `cloudsim-portal` server and the portal is
successfully talking to AWS!

1. Congrats, your cloudsim app is running successfully!

[Back to Running](Running)
