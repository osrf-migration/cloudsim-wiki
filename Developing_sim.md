[Back to Home](Home)

## Cloudsim-sim ##

### Overview ###

Cloudsim-sim is a web server. It allows Cloudsim users to start and stops gazebo.

### Life cycle ###

Typically, the Cloudsim-portal launches cloud instance that run Cloudsim-sim automatically.
There are multiple possible configurations:

* Cloudsim-sim can be running on the cloud instance
* Cloudsim-sim can be running in a docker container (inside a cloud instance)
* Cloudsim-sim can be running on a workstation (this is experimental)



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
* The ami must be shared with the correct users or made public.
* Then add the new ami to the list in
`cloudsim-widgets/app/elements/cs-machinelauncher/cs-machinelauncher.html`

[See Cloudsim-sim's API](Interface_sim)

