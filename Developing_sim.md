[Back to Home](Home)

## Cloudsim-sim ##

### Overview ###

Cloudsim-sim is a web server. It allows Cloudsim users to start and stops gazebo.

### Life cycle ###

Typically, the Cloudsim-portal launches a simulator machine that run Cloudsim-sim automatically.
There are multiple possible configurations:

* Cloudsim-sim can be running on a cloud instance (AWS instance)
* Cloudsim-sim can be running in a docker container (inside a cloud instance)
* Cloudsim-sim can be running on a workstation (this is experimental)

Normally, Cloudsim-sim should be running continuously (as a service) on the simulator machine.

Cloudsim-sim manages a list of queued simulations, and only one simulation can run at a time.


### Depends on these Cloudsim packages:

* [cloudsim-grant](https://bitbucket.org/osrf/cloudsim-grant): Uses the Javascript API.

### These Cloudsim packages depend on it:

* [gz-grant](https://github.com/osrf/gz-grant): Uses REST API.
* [gz-resources](https://github.com/osrf/gz-resources): Uses REST API.
* [cloudsim-widgets](https://bitbucket.org/osrf/cloudsim-widgets): (indirectly, it depends on `gz-*`)

### How to make changes

* Pull request to [cloudsim-sim](https://bitbucket.org/osrf/cloudsim-sim)
* Once merged into default, someone needs to ssh into a live machine to pull
the new code and then make a new ami.
* The ami must be scrubbed from ssh keys [sharing AMIs](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/building-shared-amis.html)
* The ami must be shared with the correct users or made public.
* Then add the new ami to the list in
`cloudsim-widgets/app/elements/cs-machinelauncher/cs-machinelauncher.html`

[See Cloudsim-sim's API](Interface_sim)

