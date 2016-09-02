[Back to Home](Home)

## Cloudsim-sim ##

### Depends on these Cloudsim packages:

* [cloudsim-grant](https://bitbucket.org/osrf/cloudsim-grant): Uses the Javascript API.

### These Cloudsim packages depend on it:

* [gz-cmd](https://github.com/osrf/gz-cmd): Uses websocket.
* [gz-grant](https://github.com/osrf/gz-grant): Uses REST API.
* [gz-simulationq](https://github.com/osrf/gz-simulationq): Uses REST API.
* [cloudsim-widgets](https://bitbucket.org/osrf/cloudsim-widgets): (indirectly, it depends on `gz-*`)

### How to make changes

* Pull request to [cloudsim-sim](https://bitbucket.org/osrf/cloudsim-sim)
* Once merged into default, someone needs to ssh into a live machine to pull
the new code and then make a new ami.
* The ami must be shared with the correct users or made public.
* Then add the new ami to the list in
`cloudsim-widgets/app/elements/cs-machinelauncher/cs-machinelauncher.html`

[See Cloudsim-sim's API](Interface_sim)
