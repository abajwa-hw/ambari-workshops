## Ambari Extensibility via Stacks, Views and Blueprints Workshop 

These demos are part of a webinar on Ambari. Slides and webinar recording available at http://hortonworks.com/partners/learn/
Blog article on the topics presented in the webinar is available [here](http://hortonworks.com/blog/apache-ambari-technical-workshop/)

A higher level write up of the direction of Ambari extensibility is available [here](http://hortonworks.com/blog/future-apache-ambari/)

**Want to suggest a custom Ambari service or view? Suggest [here](https://github.com/abajwa-hw/ambari-workshops/issues)**

#### Ambari Stacks/Services 
Stacks wrap services of all shapes and sizes with a consistent definition and lifecycle-control layer. With this wrapper in-place, Ambari can rationalize operations over a broad set of services.
To the Hadoop operator, this means that regardless of differences across services (e.g.install/start/stop/configure/status) each service can be managed and monitored with a consistent approach.
This also provides a natural extension point for operators and the community to create their own custom stack definitions to “plug-in” new services that can co-exist with Hadoop

- Demos:
  - Sample service (easy): 
    - [ntpd](https://github.com/abajwa-hw/ntpd-stack) - Deploy/manage time daemon from Ambari. Most basic example of how to build service using 4 files.
    - [VNC](https://github.com/abajwa-hw/vnc-stack) - remote desktop into your sandbox and start coding with Eclipse/IntelliJ on Spark/Storm
    - [Solr](https://github.com/abajwa-hw/search-demo/tree/master/solr_stack) - deploy/manage Solr from Ambari (for search)
    - [R stack](https://github.com/randerzander/r-stack) - deploy/manage R from Ambari (for data science)
  - Sample service (medium): 
    - [Node/Angular JS](https://github.com/abajwa-hw/search-demo) - deploy/manage 'Document Crawler' Angular.js webapp from Ambari (see below)
    - [Node/D3/Grunt JS](https://github.com/abajwa-hw/hdpviz) - deploy/manage 'HDFS Visualizer' D3.js webapp from Ambari (see below)
  - Sample service (harder): 
    - [iPython notebook](https://github.com/randerzander/ipython-stack) - deploy/manage iPython notebook from Ambari (for data science)
  - [Apache services (HDP 2.2)] (https://github.com/apache/ambari/tree/trunk/ambari-server/src/main/resources/stacks/HDP/2.2/services)
    

  - Security related services.  
    - [FreeIPA](https://github.com/abajwa-hw/freeipa-stack) - deploy/manage FreeIPA LDAP from Ambari (for identity management)
    - [OpenLDAP](https://github.com/abajwa-hw/openldap-stack) - deploy/manage OpenLDAP from Ambari (for identity management)
    - [Kerberos KDC](https://github.com/abajwa-hw/kdc-stack) - deploy/manage KDC from Ambari (for kerberos ticket management)
    - [NSLCD/SSSD](https://github.com/abajwa-hw/nslcd-stack) -  deploy/manage NSLCD from Ambari (to enable OS to recognize LDAP users)
    - See [steps](https://github.com/abajwa-hw/security-workshops/blob/master/Setup-kerberos-Ambari-services.md) on how to use these services to enable security from Ambari UI, with minimal command line work
    
More details on stacks/services can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Stacks+and+Services)


#### Ambari Views

Views Customizing the Interaction Experience for Operators and Users
Ambari Views will enable the community and operators to develop new ways to visualize operations, troubleshoot issues and interact with Hadoop. They will provide a framework to offer those experiences to specific sets of users. Via the pluggable UI framework, operators will be able to control which users get certain capabilities and to customize how those users interact with Hadoop.

- Demos:
  - Sample (easy): 
    - [iFrame view](https://github.com/abajwa-hw/iframe-view) (HTML only) - embed any webapp in Ambari
    - [REST API explorer view](https://github.com/abajwa-hw/blueprints-view) (HTML/basic javascript) - get started with Ambari REST APIs
    - [Apache examples](https://github.com/apache/ambari/tree/trunk/ambari-views/examples) - collection of simple Ambari Views on Apache page provided as a development guide.
    
  - Sample (medium): 
    - [Hive query view](https://github.com/randerzander/servlet-view-example) (Java servelets) - submit Hive queries from Ambari
    - [Document Crawler view](https://github.com/abajwa-hw/search-demo) (Node/Angular JS) - search through Word, PDF etc docs stored in HDFS via Ambari
    - [HDFS visualization view](https://github.com/abajwa-hw/hdpviz) (Node/D3/Grunt JS) - Navigate HDFS visually using D3 charts via Ambari
    
  - Sample (hard): 
    - [Contributed views](https://github.com/apache/ambari/tree/trunk/contrib/views). For setup instructions and screenshots click [here](https://github.com/abajwa-hw/ambari-workshops/blob/master/contributed-views.md)
	  - Hive
      - Tez
      - Files
      - Jobs
      - Capacity scheduler 
      - Slider
      - Pig
      

More details on Ambari views can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Views)

#### Ambari Blueprints

Ambari Blueprints deliver the below benefits:
A repeatable model for cluster provisioning (for consistency);
A method to automate cluster provisioning (for ad hoc cluster creation, whether bare metal or cloud);
A portable and cohesive definition of a cluster (for sharing best practices on component layout and configuration).

- Links:
  - [Apache Ambari Wiki for Blueprints](https://cwiki.apache.org/confluence/display/AMBARI/Blueprints)
  - [REST API explorer view](https://github.com/abajwa-hw/blueprints-view) to get started with APIs
  - [Sample automation](https://github.com/seanorama/ambari-bootstrap) to install/configure Ambari Agent, Ambari Server and run pre-req checks
  - [API Examples](https://github.com/seanorama/ambari-bootstrap/tree/master/api-examples) including:
    - Basics, changing password, creating blueprints, deploying clusters, changing configurations
  - [Older tutorial](http://hortonworks.com/blog/ambari-blueprints-delivers-missing-component-cluster-provisioning/)
