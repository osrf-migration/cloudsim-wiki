## Monitoring Cloudsim micro services  ##

This page discusses the OSRF Elastic Beanstalk setup. Your installation may be different.

## Login ##

You can find the relevant ssh keys in the internal wiki. Keep in mind that the cloudsim servers use the cloudsimportal.pem key (in us.east.1 region) while simulator machines are launched in the N. California (us.west.1) region, under a different account (using various ssh keys, stored in the portal db).

You need to log in the AWS console using the company credentials. Then go to the
[AWS Elastic Beanstalk](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/applications) to see the running instances.

There are 2 sets of micro services:

* The development servers (Application names end with Dev)
* The production servers (Application names end with Production)

To get to the monitoring page, first select the Application box, then select `Monitoring` on the left menu.

You can also find similar graphs on the EC2 console. Look for the individual servers in the N. Virginia (us.east.1) region, and click on the Monitoring tab once the server is selected.

## Direct links for production servers ##

Make sure you are logged in the AWS console. Then, from the same browser instance, navigate to:

* [cloudsim-auth](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/environment/monitoring?applicationName=cloudsim-auth&environmentId=e-pptrbgmrjc)
* [cloudsim-keys](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/environment/monitoring?applicationName=cloudsim-keys&environmentId=e-jwiwgfh6j7)
* [cloudsim-portal](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/environment/monitoring?applicationName=cloudsim-portal&environmentId=e-kxqrpqema2)
* [cloudsim-widgets](https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/environment/monitoring?applicationName=cloudsim-widgets&environmentId=e-6i3zjjqd3m)

Simulator instances are launched on demand, and must be monitored from the EC2 console.