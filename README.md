## Ambari Extensibility via Stacks, Views and Blueprints Workshop 

These demos are part of a webinar on Ambari. Slides and webinar recording available at http://hortonworks.com/partners/learn/
Blog article on the topics presented in the webinar is available [here](http://hortonworks.com/blog/apache-ambari-technical-workshop/)

A higher level write up of the direction of Ambari extensibility is available [here](http://hortonworks.com/blog/future-apache-ambari/)

**Want to suggest a custom Ambari service or view? Suggest [here](https://github.com/abajwa-hw/ambari-workshops/issues)**

#### Ambari Stack Services 
Stacks wrap services of all shapes and sizes with a consistent definition and lifecycle-control layer. With this wrapper in-place, Ambari can rationalize operations over a broad set of services.
To the Hadoop operator, this means that regardless of differences across services (e.g.install/start/stop/configure/status) each service can be managed and monitored with a consistent approach.
This also provides a natural extension point for operators and the community to create their own custom stack definitions to “plug-in” new services that can co-exist with Hadoop
Documentation on stacks/services can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Stacks+and+Services)

##### General services
| Service name	| Git | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| ntpd | [abajwa](https://github.com/abajwa-hw/ntpd-stack)  | Beginner | Deploy/manage time daemon from Ambari |  Most basic 'master' service example of how to wrap Ambari service around linux service  |
| Maven | [randerzander](https://github.com/randerzander/maven-stack) |  Beginner | Deploy the bits for this developer tool on a cluster | Most basic 'client' service example of how to use Ambari to install custom bits on cluster |
| VNC  | [abajwa](https://github.com/abajwa-hw/vnc-stack) | Easy | deploy VNC service and developer tools | Remote desktop into your sandbox and start coding with Eclipse/IntelliJ on Spark/Storm | 
| Solr  | [abajwa](https://github.com/abajwa-hw/search-demo/tree/master/solr_stack) | Easy | deploy/manage Solr from Ambari  | Useful for search use cases on Hadoop | 
| HDFS Vizualizer | [Node/D3/Grunt JS](https://github.com/abajwa-hw/hdpviz) | Medium | deploy/manage D3.js webapp from Ambari | Inspired by [Twitters HDFS du project](https://blog.twitter.com/2012/visualizing-hadoop-with-hdfs-du) |
| Document crawler | [Node/Angular JS](https://github.com/abajwa-hw/search-demo) | Medium | deploy/manage Angular.js webapp from Ambari | Demo for search workshop |
| Official component services | [Apache](https://github.com/apache/ambari/tree/trunk/ambari-server/src/main/resources/stacks/HDP/2.2/services)| Advanced | Browse the code for the HDP services | Kafka and Knox are good examples to follow |

##### Data science related services 
| Service name	| Git | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| R | [randerzander](https://github.com/randerzander/r-stack) | Easy | deploy/manage R from Ambari | Useful for data science use cases on Hadoop |
| iPython notebook | [randerzander](https://github.com/randerzander/ipython-stack) | Medium | deploy/manage iPython notebook from Ambari | Useful for data science use cases on Hadoop |
    
##### Security related services 
| Service name	| Git | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| FreeIPA | [abajwa](https://github.com/abajwa-hw/freeipa-stack) | Easy | deploy/manage FreeIPA LDAP from Ambari | For deploying combined LDAP/KDC for Identity Management |
| OpenLDAP | [abajwa](https://github.com/abajwa-hw/openldap-stack) | Medium | deploy/manage OpenLDAP from Ambari | For deploying combined LDAP for Identity Management |
| Kerberos KDC | [abajwa](https://github.com/abajwa-hw/kdc-stack) | Easy | deploy/manage KDC from Ambari | For kerberos ticket management |
| NSLCD/SSSD | [abajwa](https://github.com/abajwa-hw/nslcd-stack) | Easy | deploy/manage NSLCD from Ambari | to enable OS to recognize LDAP users |

- See [guide](https://github.com/abajwa-hw/security-workshops/blob/master/Setup-kerberos-Ambari-services.md) on how to use these services to enable security from Ambari UI, with minimal command line work



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
