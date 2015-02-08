## Ambari Extensibility via Stacks, Views and Blueprints Workshop 

These demos are part of an upcoming Ambari webinar.

Slides and webinar recording will be available at http://hortonworks.com/partners/learn/

A higher level write up of the direction of Ambari extensibility is available [here](http://hortonworks.com/blog/future-apache-ambari/)

#### Ambari Stacks 
Stacks wrap services of all shapes and sizes with a consistent definition and lifecycle-control layer. With this wrapper in-place, Ambari can rationalize operations over a broad set of services.
To the Hadoop operator, this means that regardless of differences across services (e.g.install/start/stop/configure/status) each service can be managed and monitored with a consistent approach.
This also provides a natural extension point for operators and the community to create their own custom stack definitions to “plug-in” new services that can co-exist with Hadoop

- Demos:
  - Sample service (easy): 
    - [VNC](https://github.com/abajwa-hw/vnc-stack)
    - [Solr](https://github.com/abajwa-hw/search-demo/tree/master/solr_stack)
  - Sample service (medium): 
    - [Angular JS](https://github.com/abajwa-hw/search-demo)
  - Sample service (harder): 
    - [iPython notebook](https://github.com/randerzander/ipython-stack) 

  - Security related services: 
    - [FreeIPA](https://github.com/abajwa-hw/freeipa-stack)
    - [OpenLDAP](https://github.com/abajwa-hw/openldap-stack)
    - [Kerberos KDC](https://github.com/abajwa-hw/kdc-stack)
    
More details on stacks/services can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Stacks+and+Services)


#### Ambari Views

Views Customizing the Interaction Experience for Operators and Users
Ambari Views will enable the community and operators to develop new ways to visualize operations, troubleshoot issues and interact with Hadoop. They will provide a framework to offer those experiences to specific sets of users. Via the pluggable UI framework, operators will be able to control which users get certain capabilities and to customize how those users interact with Hadoop.

- Demos:
  - Sample (easy): 
    - [iFrame view](https://github.com/abajwa-hw/iframe-view)
    - [REST API explorer view](https://github.com/abajwa-hw/blueprints-view) which use only HTML/javascript
  - Sample (medium): 
    - [Hive query view](https://github.com/randerzander/servlet-view-example) which uses Java servelets
  - Sample (hard): 
    - [Contributed views](https://github.com/apache/ambari/tree/trunk/contrib/views). For setup instructions and screenshots click [here](https://github.com/abajwa-hw/ambari-workshops/blob/master/contributed-views.md)
      - Tez
      - Files
      - Jobs
      - Capacity scheduler 
      - Slider
      - Pig
      

More details can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Views)

#### Ambari Blueprints

Ambari Blueprints deliver the below benefits:
A repeatable model for cluster provisioning (for consistency);
A method to automate cluster provisioning (for ad hoc cluster creation, whether bare metal or cloud);
A portable and cohesive definition of a cluster (for sharing best practices on component layout and configuration).

More details can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Blueprints)

- Demos:
  - Sample (easy): [REST API explorer view](https://github.com/abajwa-hw/blueprints-view)
  - [Tutorial](http://hortonworks.com/blog/ambari-blueprints-delivers-missing-component-cluster-provisioning/)
   
