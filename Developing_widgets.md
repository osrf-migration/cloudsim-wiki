[Back to Home](Home)

# Developing the GUI

CloudSim's GUI uses the
[Polymer](https://www.polymer-project.org/1.0/)
platform for web components.

CloudSim is composed of several web-components, each of them performing one
especialized task. The components are divided into two groups, according to
their prefix: `gz-` or `cs-`.

# Component types

## gz-*

The `gz-` components:

* Provide an interface to servers.
* Are not meant to display information.
* Expose a clear and simple API which which other components can use.
* Are general and not tied to the cloudsim app.
* Each component is hosted at its own repository and can be released separately.
* When released, any polymer app can use the component simply by referencing it
in `bower.json`. No need to clone the repo.

[Here](https://github.com/osrf?utf8=%E2%9C%93&query=gz-) you can see all `gz-`
components.

## cs-*

`cs-` components:

* Are specific for the cloudsim app.
* Handle very little logic, are there mostly to display and organize information.
* Have no direct communication with servers.
* Are all hosted in the
[cloudsim-widgets](https://bitbucket.org/osrf/cloudsim-widgets/src/99d0846b744cb4c5932713d9dea399ffd3535d7c/app/elements/?at=default)
repository.

## gz-account + cs-signuppage example

* Target server: `cloudsim-auth`

* Purpose: create and remove accounts

* [`gz-account`](https://github.com/osrf/gz-accounts/blob/master/gz-accounts.html)
's role: Send REST requests to the server.

* [`cs-signuppage`](https://bitbucket.org/osrf/cloudsim-widgets/src/default/app/elements/cs-signuppage/cs-signuppage.html)
's role: User interface for input and feedback.

* Usage:

  1. Import both components in [`app/elements/elements.html`](https://bitbucket.org/osrf/cloudsim-widgets/src/99d0846b744cb4c5932713d9dea399ffd3535d7c/app/elements/elements.html?fileviewer=file-view-default):

        <link rel="import" href="../bower_components/gz-accounts/gz-accounts.html">
        <link rel="import" href="cs-signuppage/cs-signuppage.html">

  1. Instantiate `gz-accounts` within `cs-signuppage`. The parameters passed in
  were the auth server's `url` and a callback for when registration is complete
  (`on-register`).

        <gz-accounts
          id="accounts"
          url={{url}}
          on-register="onRegister"
        ></gz-accounts>


  1. `cs-signuppage` provides input fields for name and password:

        <paper-input label="User name" id="user"></paper-input>
        <paper-input label="Password" id="pass1" type="password"></paper-input>
        <paper-input label="Confirm password" id="pass2" type="password"></paper-input>

  1. Once the user submits, `cs-signuppage` calls `gz-accounts`'s function:

        this.$.accounts.registerUser(user, pass);

  1. When the account has been created, `gz-accounts` fires an event which
  triggers the `onRegister` callback in `cs-signuppage`.

  1. `cs-signuppage` fires an event so the toast notifies success or error.

# Development

Let's walk through the process of adding a component to `cloudsim-widgets`.
We'll be covering **the case where no changes to other servers are needed**. This
is the case when adding static content, reorganizing existing functionality or
adding visualization for features already exposed by the servers, but not yet
displayed in the GUI.

## Use public servers

Since our focus is on the widgets side, we don't need to worry about launching
local auth and portal servers. So we can set our cloudsim-widgets `.env` file
to use the public servers as explained [earlier](Running).

> When using the public server, be mindful of machines that had been launched
> before you started, other developers might be working on them.

## Run the server

First move into the widgets directory:

    cd cloudsim-widgets

There are two ways to run the servers:

* `gulp serve`: Good for debugging, but slow.

* `gulp serve:dist`: Good for production, all the code is optimized in a process
called "vulcanize".

## BrowserSync

By default, BrowserSync is at work while the server is up. Whenever you make a
change to the source code, the browser will refresh and you can see the results
immediately.

Another BrowserSync feature is that whatever you do in one browser will be
reflected on all other open browsers running the app. This might make it
difficult to test two different users at the same time, and can cause some
actions to be performed twice if you accidentaly forgot another browser open.

You can configure BrowserSync at [http://localhost:3001/](http://localhost:3001/).

### Adding a `cs-` component

1.



## gz-XXX ##

### Updates ###

* Pull request to [gz-XXX](https://github.com/osrf/?utf8=%E2%9C%93&query=gz-).
* Once merged into default, make a new release through GitHub.

### Impacted repos ###

The following repos might need code updates or redeployment to take
gz-XXX changes into account.

* [cloudsim-widgets](https://bitbucket.org/osrf/cloudsim-widgets)

