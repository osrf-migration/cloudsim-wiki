## Brief overview of Linux performance investigation tools ##

![linux_perf_tools_full.png](https://bitbucket.org/repo/eaE4bR/images/1483166042-linux_perf_tools_full.png)

## Linux  Performance Analysis in 60 seconds ##

[[embed url=http://www.youtube.com/watch?v=ZdVpKx6Wmc8]]

## Methodology ##


### Has the machine performed better before? 

### USE for every resource:

* Utilization
* Staturation
* Errors

Example of resources: CPU, Network devices, Disks... also include busses and interconnects.

![linux use method](http://www.brendangregg.com/USEmethod/use-linux.html)

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

### sudo, yum ###

Yum is crippled on Amazon ec2, you are on your own.

### where is the node app? ###

`cd /var/app/current`

### where is the node log? ###

`tail -f /var/log/nodejs/nodejs.log`

### where is the node app? ###

`/opt/elasticbeanstalk/node-install/node-v6.2.2-linux-x64/bin/node`

### where is the redis client? ###

`./redis-2.8.4/src/redis-cli`