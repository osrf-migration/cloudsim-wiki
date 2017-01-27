## Brief overview of Linux performance investigation tools ##

![linux_perf_tools_full.png](https://bitbucket.org/repo/eaE4bR/images/1483166042-linux_perf_tools_full.png)

## Linux  Performance Analysis in 60 seconds ##

[[embed url=http://www.youtube.com/watch?v=ZdVpKx6Wmc8]]

## Bandwidth monitoring using nload ##
bandwidth monitoring using nload:

`sudo apt install nload`

get your ip:
`curl checkip.amazonaws.com`
 
get your network device:
`ifconfig` 

monitor bandwidth (on device eth0):

`nload eth0`
 

## EC2 Linux ## 

Elastic Beanstalk machines run the Amazon Linux distribution (a Fedora like system, with Yum package manager)

https://bitbucket.org/osrf/cloudsim/wiki/Deployment

`tail -f /var/log/nodejs/nodejs.log`

`/opt/elasticbeanstalk/node-install/node-v6.2.2-linux-x64/bin/node`