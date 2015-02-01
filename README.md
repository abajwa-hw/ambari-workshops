## Ambari Stacks, Views and Blueprints Workshop 

These demos are part of an upcoming Ambari webinar.

Slides and webinar recording are available at http://hortonworks.com/partners/learn/

A higher level write up of the direction of Ambari is available [here](http://hortonworks.com/blog/future-apache-ambari/)

#### Ambari Stacks 
Stacks wrap services of all shapes and sizes with a consistent definition and lifecycle-control layer. With this wrapper in-place, Ambari can rationalize operations over a broad set of services.
To the Hadoop operator, this means that regardless of differences across services (e.g.install/start/stop/configure/status) each service can be managed and monitored with a consistent approach.
This also provides a natural extension point for operators and the community to create their own custom stack definitions to “plug-in” new services that can co-exist with Hadoop

Sample service (easy): [VNC](https://github.com/abajwa-hw/vnc-stack) or [IPA](https://github.com/abajwa-hw/freeipa-stack) or [Solr](https://github.com/abajwa-hw/search-demo/tree/master/solr_stack)
Sample service (medium): [Angular JS](https://github.com/abajwa-hw/search-demo)
Sample service (harder): [iPython notebook](https://github.com/randerzander/ipython-stack) 


More details can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Stacks+and+Services)


#### Ambari Views

Views Customizing the Interaction Experience for Operators and Users
Ambari Views will enable the community and operators to develop new ways to visualize operations, troubleshoot issues and interact with Hadoop. They will provide a framework to offer those experiences to specific sets of users. Via the pluggable UI framework, operators will be able to control which users get certain capabilities and to customize how those users interact with Hadoop.

Ambari view to embed/integrate with other products
Sample (easy): [iFrame view](https://github.com/abajwa-hw/iframe-view)
Sample (medium): [Hive query view](https://github.com/randerzander/servlet-view-example)
Sample (hard): [Contributed views](https://github.com/apache/ambari/tree/trunk/contrib/views)

More details can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Views)

#### Ambari Blueprints

Ambari Blueprints deliver the below benefits:
A repeatable model for cluster provisioning (for consistency);
A method to automate cluster provisioning (for ad hoc cluster creation, whether bare metal or cloud);
A portable and cohesive definition of a cluster (for sharing best practices on component layout and configuration).

More details can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Blueprints)


