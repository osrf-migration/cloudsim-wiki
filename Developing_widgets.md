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

The `gz-` components provide an interface to servers. They are not meant to be
used to display information, instead, they expose a clear and simple API which
which other components can use.

`gz-` components are general and not tied to the cloudsim app. Each component
is hosted at its own repository and can be released separately. When released,
any polymer user can use the component simply by referencing it in their
`bower.json`.

[Here](https://github.com/osrf?utf8=%E2%9C%93&query=gz-) you can see all `gz-`
components.

### `gz-token` example

* Target server: cloudsim-auth

* Purpose: create and remove accounts

* Usage in cloudsim-widgets:

1. Import it in [`app/elements/elements.html`](https://bitbucket.org/osrf/cloudsim-widgets/src/99d0846b744cb4c5932713d9dea399ffd3535d7c/app/elements/elements.html?fileviewer=file-view-default):

      <link rel="import" href="../bower_components/gz-accounts/gz-accounts.html">

1. [cs-signuppage](https://bitbucket.org/osrf/cloudsim-widgets/src/99d0846b744cb4c5932713d9dea399ffd3535d7c/app/elements/cs-signuppage/cs-signuppage.html?fileviewer=file-view-default) instantiates the element:

      <gz-accounts
        id="accounts"
        url={{url}}
        on-register="onRegister"
      ></gz-accounts>

    The parameters passed in were the auth server's `url` and a callback for
    when registration is complete (`on-register`).

1. Now all `cs-signuppage` must do to request a new account to be created is
calling:

    this.$.accounts.registerUser(user, pass);

1. And when the account has been created, `onRegister` will be called.

## cs-*

`cs-` components are meant to be very specific for the cloudsim app. They handle
very little logic, no direct server communication, and are there mostly to
display and organize information. They are all hosted in the
[cloudsim-widgets](https://bitbucket.org/osrf/cloudsim-widgets/src/99d0846b744cb4c5932713d9dea399ffd3535d7c/app/elements/?at=default)
repository.

An example is the `cs-signuppage` listed above.

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

