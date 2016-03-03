## Ambari Extensibility via Stacks, Views and Blueprints Workshop 

These demos are part of a webinar on Ambari. 
- Slides and webinar recording available at http://hortonworks.com/partners/learn/#ambari
- Blog article on the topics presented in the webinar is available [here](http://hortonworks.com/blog/apache-ambari-technical-workshop/)
- A higher level blog about the direction of Ambari extensibility is available [here](http://hortonworks.com/blog/future-apache-ambari/)
- Ambari roadmap is also available on the [wiki](https://github.com/apache/ambari/tree/trunk/ambari-server/src/main/resources/common-services/HBASE/0.96.0.2.0)

**Want to suggest a custom Ambari service or view? Suggest [here](https://github.com/abajwa-hw/ambari-workshops/issues)**

#### Contents
- [Ambari stack services](https://github.com/abajwa-hw/ambari-workshops#ambari-stack-services)
- [Ambari Views](https://github.com/abajwa-hw/ambari-workshops#ambari-views)
- [Ambari Blueprints/APIs](https://github.com/abajwa-hw/ambari-workshops#ambari-blueprintsapis)

--------------------

#### Ambari Stack Services 
Stacks wrap services of all shapes and sizes with a consistent definition and lifecycle-control layer. With this wrapper in-place, Ambari can rationalize operations over a broad set of services.
To the Hadoop operator, this means that regardless of differences across services (e.g.install/start/stop/configure/status) each service can be managed and monitored with a consistent approach.
This also provides a natural extension point for operators and the community to create their own custom stack definitions to “plug-in” new services that can co-exist with Hadoop
Documentation on stacks/services can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Stacks+and+Services)

##### Sample services (general)
| Service name	| Github url/author | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| [ntpd](http://www.ntp.org) | [abajwa](https://github.com/abajwa-hw/ntpd-stack)  | Beginner | Deploy/manage time daemon from Ambari |  Most basic 'master' service example of how to wrap Ambari service around linux daemon service, using 4 files |
| [Maven](http://maven.apache.org) | [randerzander](https://github.com/randerzander/maven-stack) |  Beginner | Deploy the bits for this developer tool on a cluster | Most basic 'client' service example of how to use Ambari to install software bits on cluster (w/o starting a daemon service)  |
| [VNC](http://en.wikipedia.org/wiki/Virtual_Network_Computing)  | [abajwa](https://github.com/abajwa-hw/vnc-stack) | Easy | deploy VNC service and developer tools | Remote desktop into your sandbox and start coding with Eclipse/IntelliJ on Spark/Storm | 
| [OpenTSDB](http://opentsdb.net) | [abajwa](https://github.com/abajwa-hw/opentsdb-service) | Easy | Deploy/monitor timeseries DB on top of HBase |  Implement your own Google Finance-like functionality on HDP |
| HDFS Vizualizer | [abajwa](https://github.com/abajwa-hw/hdpviz) | Medium | deploy/manage D3.js webapp from Ambari | Inspired by [Twitters HDFS du project](https://blog.twitter.com/2012/visualizing-hadoop-with-hdfs-du) - see below for view details. Another *custom* service example|
| Document crawler | [abajwa](https://github.com/abajwa-hw/search-demo) | Medium | deploy/manage Angular.js webapp from Ambari | search through Word, PDF etc docs stored in HDFS via Ambari - see below for view details. Another *custom* service example |
| Official component services | [Apache](https://github.com/apache/ambari/tree/trunk/ambari-server/src/main/resources/stacks/HDP/2.2/services)| Advanced | Browse the code for the HDP services | Kafka and Knox are good examples to follow |

##### Data science related sample services 
| Service name	| Github url/author | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| [R](http://www.r-project.org) | [randerzander](https://github.com/randerzander/r-stack) | Easy | deploy/manage R from Ambari | Another example of a 'client' service which is useful for data science use cases on Hadoop |
| [iPython notebook](http://ipython.org/notebook.html) | [randerzander](https://github.com/randerzander/ipython-stack) | Medium | deploy/manage iPython notebook from Ambari | Useful for data science use cases on Hadoop |
| [Zeppelin notebook](https://zeppelin.incubator.apache.org) | [abajwa](https://github.com/abajwa-hw/zeppelin-stack) | Medium | deploy/manage Zeppelin notebook from Ambari | Useful for data science use cases on Hadoop |
    
##### Security related sample services 
| Service name	| Github url/author | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| [FreeIPA](http://www.freeipa.org) | [abajwa](https://github.com/abajwa-hw/freeipa-stack) | Easy | deploy/manage FreeIPA LDAP from Ambari | For deploying combined LDAP/KDC for Identity Management |
| [Kerberos KDC](http://web.mit.edu/kerberos/) | [abajwa](https://github.com/abajwa-hw/kdc-stack) | Easy | deploy/manage KDC from Ambari | For kerberos ticket management |
| [NSLCD/SSSD](http://arthurdejong.org/nss-pam-ldapd/nslcd.conf.5) | [abajwa](https://github.com/abajwa-hw/nslcd-stack) | Easy | deploy/manage NSLCD from Ambari | to enable OS to recognize LDAP users |
| [OpenLDAP](http://www.openldap.org) | [abajwa](https://github.com/abajwa-hw/openldap-stack) | Medium | deploy/manage OpenLDAP from Ambari | For deploying combined LDAP for Identity Management |

- See [guide](https://github.com/abajwa-hw/security-workshops/blob/master/Setup-kerberos-Ambari-services.md) on how to use these services to enable security from Ambari UI, with minimal command line work
- **NEW** See [guide](https://github.com/abajwa-hw/ambari-workshops/blob/master/blueprints-demo-security.md) on how to deploy these services via a Blueprint to easily setup a kerborized cluster with LDAP/PAM

##### Search related services 
| Service name	| Github url/author | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| [Solr](http://lucene.apache.org/solr/)  | [abajwa](https://github.com/abajwa-hw/solr-stack) | Easy | deploy/manage Solr from Ambari  | Detailed example of a *custom* Ambari service that uses pidfiles to monitor the service. Will be productized by our partner LucidWorks (see below) | 
| [Elastic Search](https://www.elastic.co/)  | [saurabhmishra](https://github.com/saurabhmishra/ambarielasticsearch) | Medium | deploy/manage ElasticSearch from Ambari  |  | 


##### Partner contributed  
| Service name	| Github url/author | Difficulty	| Description	| Comments	|
| ------------- | ----- | ---------- 	| ------------  | --------  |
| [Tachyon](http://tachyon-project.org/) | [seraphin](https://github.com/seraphin/tachyon-service) | Medium | deploy/manage Tachyon from Ambari | Service to manage Tachyon in cluster mode |
| [KPMG Analytics and Visualization Environment](https://github.com/KaveIO/AmbariKave/wiki) | [KaveIO](https://github.com/KaveIO/AmbariKave/wiki) | Medium | KPMG Analytics and Visualization Environment | The KAVE combines the power of a Lambda Stack, with a development line and core analysis tools. |
| [Solr](https://github.com/LucidWorks/solr-stack)| [LucidWorks](https://github.com/LucidWorks/solr-stack) | Easy | deploy/manage Solr from Ambari | Will be added  to HDP in future | 
| [Cask](http://cask.co/)|[Cask service](https://github.com/caskdata/ambari-cdap-service)| Medium | Deploy Cask |  |
| [MongoDB](https://www.mongodb.org/)|[nikunjness](https://github.com/nikunjness/mongo-ambari)| Easy | Deploy Mongo | |
| [Redis](http://redis.io/)|[nikunjness](https://github.com/nikunjness/redis-ambari)| Easy | Deploy Redis | |

##### Integration with Ambari Metrics

- In Ambari 2.1 onwards, custom services can push their metrics to Ambari Metrics service and define their own widgets.  Documentation [here](https://cwiki.apache.org/confluence/display/AMBARI/Metrics+Collector+API+Specification)


The Onyara team recently did this integration for Apache Nifi. Blog and code samples below:
- http://bryanbende.com/development/2015/07/31/ambari-metrics-part1-metrics-collector/
- http://bryanbende.com/development/2015/08/16/ambari-metrics-part2-service-definition/


Code samples:
- [Simple metric producer](https://github.com/bbende/ambari-metric-producer)
- [Nifi metrics producer](https://github.com/apache/nifi/tree/master/nifi-nar-bundles/nifi-ambari-bundle/nifi-ambari-reporting-task)
- Nifi metrics/widgets
  - https://github.com/abajwa-hw/ambari-nifi-service/blob/master/metrics.json
  - https://github.com/abajwa-hw/ambari-nifi-service/blob/master/widgets.json
- [HDFS metrics/widgets](https://github.com/apache/ambari/tree/trunk/ambari-server/src/main/resources/common-services/HDFS/2.1.0.2.0)

##### Automated Kerberos setup

Ambari supports services automating kerberos setup. More details available at: https://cwiki.apache.org/confluence/display/AMBARI/Automated+Kerberizaton

##### Enhanced configs

- In Ambari 2.1 onwards, custom services can define enhanced configurations (similar to HDFS, YARN etc) to make their configuration panel look native. More details available in [wiki](https://cwiki.apache.org/confluence/display/AMBARI/Enhanced+Configs)

Code samples:
- [Hive](https://github.com/apache/ambari/blob/8967ed9bc8967f6f6783c16f6403a3de0a0b2792/ambari-server/src/main/resources/stacks/HDP/2.2/services/HIVE/themes/theme.json)
- [HDFS](https://github.com/apache/ambari/blob/291b7cbf5852db3fa37f4f180158d0958241e05b/ambari-server/src/main/resources/stacks/HDP/2.2/services/HDFS/themes/theme.json)
- [YARN](https://github.com/apache/ambari/blob/291b7cbf5852db3fa37f4f180158d0958241e05b/ambari-server/src/main/resources/stacks/HDP/2.2/services/YARN/themes/theme.json)

##### Developer FAQ:

- How to enable debug logging?

In /etc/ambari-agent/conf/ambari-agent.ini set loglevel=DEBUG and run ‘service ambari-agent restart'

- How to test your service outside of Ambari?

After enabling debugging you can see the full command that Ambari invokes for each of the INSTALL, START, STOP operations for your service which can be run from the command line e.g.  
While you are installing service via wizard the below will give the full commands to invoke master.py:
```
ps -ef | grep <servicename>
```

e.g.
```
/usr/bin/python2.6 /var/lib/ambari-agent/cache/stacks/HDP/2.3/services/zeppelin-stack/package/scripts/master.py INSTALL /var/lib/ambari-agent/data/command-2502.json /var/lib/ambari-agent/cache/stacks/HDP/2.3/services/zeppelin-stack/package /var/lib/ambari-agent/data/structured-out-2502.json INFO /var/lib/ambari-agent/data/tmp
```

- In case service install fails, how to delete/unregister it from Ambari?

You will have to manually remove any artifacts created by service. To unregister the service from Ambari, see example here: https://github.com/hortonworks-gallery/ambari-zeppelin-service#remove-zeppelin-service

--------------------

#### Ambari Views

Views Customizing the Interaction Experience for Operators and Users
Ambari Views will enable the community and operators to develop new ways to visualize operations, troubleshoot issues and interact with Hadoop. They will provide a framework to offer those experiences to specific sets of users. Via the pluggable UI framework, operators will be able to control which users get certain capabilities and to customize how those users interact with Hadoop.
Documentation on Ambari views can be found [here](https://cwiki.apache.org/confluence/display/AMBARI/Views)

##### Sample views

| View name	| Github url/author | Difficulty	| Description	| Comments	|
| --------- | ----- | -------- 	| ------------  | --------  |
| [iFrame](http://www.w3schools.com/html/html_iframe.asp)  | [abajwa](https://github.com/abajwa-hw/iframe-view) | Beginner | embed any webapp within Ambari | Most basic example of how to build an HTML only view, using 3 files |
| REST API Explorer  | [abajwa](https://github.com/abajwa-hw/blueprints-view) | Easy |  get started with Ambari REST APIs | Similar to above but also includes basic javascript |
| [Hive](https://cwiki.apache.org/confluence/display/Hive/Home) query | [randerzander](https://github.com/randerzander/servlet-view-example) | Medium | submit Hive SQL from Ambari | Basic example of java servlet view |
| Document Crawler | [pcodding](https://github.com/abajwa-hw/search-demo) | Medium | search through Word, PDF etc docs stored in HDFS via Ambari | Example of view written in Node.js/Angular JS |
| HDFS visualizer | [dp1140a](https://github.com/abajwa-hw/hdpviz) | Medium | Navigate HDFS visually using D3 charts via Ambari | Node/D3/Grunt JS webapp that invokes WebHDFS APIs. Inspired by [Twitters HDFS du project](https://blog.twitter.com/2012/visualizing-hadoop-with-hdfs-du) |
| Phoenix metrics charts | [randerzander](https://github.com/randerzander/rt-view) | Meduim | An example of an Ambari View with a simple UI for polling Phoenix and displaying realtime metrics. | |
| Apache sample views | [Apache](https://github.com/apache/ambari/tree/trunk/ambari-views/examples) | Varying | Sample views from Apache Ambari page | Starts with examples of basic html views and advances to java servlet views with configs|

##### Contributed views

[Contributed views](https://github.com/apache/ambari/tree/trunk/contrib/views) below will be TP in upcoming version of Ambari. For setup instructions and screenshots click [here](https://github.com/abajwa-hw/ambari-workshops/blob/master/contributed-views.md)
  - Hive
  - Tez
  - Files
  - Jobs
  - Capacity scheduler 
  - Slider
  - Pig
      

------------------------


#### Ambari Blueprints/APIs

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
  - [Guide](https://github.com/abajwa-hw/ambari-workshops/blob/master/blueprints-demo-security.md) on how to deploy custom services via a Blueprint to easily setup a kerborized cluster with OpenLDAP/NSLCD/KDC
  - [Older tutorial](http://hortonworks.com/blog/ambari-blueprints-delivers-missing-component-cluster-provisioning/)
  
