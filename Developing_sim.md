[Back to Home](Home)

Explain the process involved in making a change to cloudsim-sim,
generating a new ami, sharing that with the correct users and making
that available in the GUI.

### Updates ###

* Pull request to [cloudsim-sim](https://bitbucket.org/osrf/cloudsim-sim)
* Once merged into default, someone needs to ssh into a live machine to pull
the new code and then make a new ami.
* Then add the new ami to the list in
`cloudsim-widgets/app/elements/cs-machinelauncher/cs-machinelauncher.html`

### Impacted repos ###

The following repos might need code updates or redeployment to take
cloudsim-sim changes into account.

* [cloudsim-widgets](https://bitbucket.org/osrf/cloudsim-widgets)
* [gz-XXX](https://github.com/osrf/?utf8=%E2%9C%93&query=gz-)


