# CloudSim

## What is CloudSim? ##

The DARPA Virtual Robotics Challenge gave birth to the first version of CloudSim. It provided a centralized platform that facilitated teams of participants from around the world to compete in simulation simultaneously. Since then, various projects have demanded the need for a similar cloud hosted environment for robotics competitions. In this presentation, we reveal a new, redesigned CloudSim that aims to be a generic tool for running robotics software and simulations on the cloud. We present some of its key features including simulation instance sharing, reusable front-end web components, a WebGL visualization client, and security and authentication.

### Roscon presentation ###

[Video](https://vimeo.com/187696089)
[Slides](http://roscon.ros.org/2016/presentations/ROSCon2016_Cloudsim.pdf)


## Installation

1. [Installation](Installation)

    Instructions on how to get dependencies, clone all required repositories
    and link them against each other.

1. [Running](Running)

    Instructions on how to configure the environments for all servers and launch
    them all locally at once.

1. [Deployment](Deployment)

    Instructions on how to deploy servers using AWS Elastic Beanstalk and Codeship.

## Development

### Building blocks

1. [cloudsim-widgets + gz-*](Developing_widgets)

    Explains the process of making changes to the graphical user interface and
    having those reflected on the live website.

1. [cloudsim-portal](Developing_portal)

    Explains the process of making changes to the portal server, which manages
    users and talks to AWS, and having the changes reflected on the live server.

1. [cloudsim-auth](Developing_auth)

    Explains the process of making changes to the authentication server and
    making those changes live.

1. [cloudsim-sim](Developing_sim)

    Explains the process of making changes to the server which goes on the
    machines launched through AWS.

1. [cloudsim-grant](Developing_grant)

    Explains the process of making changes to the grant middleware, which is used by cloudsim-sim and i
    cloudsim-portal to manage user permissions and (some?) data.

1. [cloudsim-keys](Developing_keys)

    Explains the process of making changes to the server which serves keys to the simulators.

## Operation

1.  [AWS console monitoring](Aws_console_monitoring)

1.  [Linux performance](Linux_performance)

### Interfaces

* [Resource model](Resource_model): Overview of the resource model shared by all
servers.
* [Server structure](Server structure): Overview of a typical server.

The following pages describe the API for each block.

1. [cloudsim-auth](Interface_auth)

1. [cloudsim-portal](Interface_portal)

1. [cloudsim-sim](Interface_sim)

1. [cloudsim-widgets](Interface_widgets)

1. [cloudsim-keys](Interface_keys)

1. gz- web components

    * [gz-accounts](https://osrf.github.io/gz-accounts/components/gz-accounts/)

    * [gz-cmd](https://osrf.github.io/gz-cmd/components/gz-cmd/)

    * [gz-grant](https://osrf.github.io/gz-grant/components/gz-grant/)

    * [gz-simulationq](https://osrf.github.io/gz-simulationq/components/gz-simulationq/)

    * [gz-simulatorlauncher](https://osrf.github.io/gz-simulatorlauncher/components/gz-simulatorlauncher/)

    * [gz-simulatorq](https://osrf.github.io/gz-simulatorq/components/gz-simulatorq/)

    * [gz-token](https://osrf.github.io/gz-token/components/gz-token/)