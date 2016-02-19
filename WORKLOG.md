# Skyport 4 Work Log

Pohsun Huang(pohsun@infinitiessoft.com)
Tata Chen(tata@infinitiessoft.com)

we have decided to keep a record of our work on Skyport 4 here in the repo. It can be removed when the project goes live, but will serve as a handy log of what I'm doing and thinking during development.

### TODO

* add volume, nic, snapshot, console, apis

### 19th February 2016

* Refactor nova2.0-api and wrtie the Openstack Driver Usages of implemented api:versions, limits, availability zone
* add nova2.0-api resource : os-availability-zone

### 18th February 2016

* Refactor nova2.0-api and wrtie the Openstack Driver Usages of implemented api:server_ips, server_metadata, image_metadata.
* add nova2.0-api resource : loadbalancers

### 17th February 2016

* Refactor nova2.0-api
* Move keystone middleware code to keystone4j-client 
* wrtie the Openstack Driver of implemented api: servers, servers_action, flavors, images, networks.
* add nova2.0-api : networks, subnets
