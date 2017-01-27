## Monitoring Cloudsim micro services  ##

This page discusses the OSRF Elastic Beanstalk setup. Your installation may be different.

## Login ##

You need to log in the AWS console using the company credentials. Then go to the
[AWS Elastic Beanstalk](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/applications) to see the running instances.

There are 2 sets of micro services:

* The development servers (Application names end with Dev)
* The production servers (Application names end with Production)

To get to the monitoring page, first select the Application box, then select `Monitoring` on the left menu.

* [cloudsim-widgets](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/environment/monitoring?applicationName=cloudsim-widgets&environmentId=e-6i3zjjqd3m)