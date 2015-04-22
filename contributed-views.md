# Contributed Ambari Views 

## Contents
  - [Prebuilt sandbox VM](https://github.com/abajwa-hw/ambari-workshops/blob/master/contributed-views.md#ambari-20-sandbox)
  - [Views screenshots](https://github.com/abajwa-hw/ambari-workshops/blob/master/contributed-views.md#views-screenshots)
  - [Setup views on existing cluster](https://github.com/abajwa-hw/ambari-workshops/blob/master/contributed-views.md#setup-instructions-for-contributed-views)
  - [Install Ambari 2.0 from scratch](https://github.com/abajwa-hw/security-workshops/blob/master/Setup-kerberos-Ambari.md)
  - [Try new Ambari 2.0 security wizard](https://github.com/abajwa-hw/security-workshops/blob/master/Setup-kerberos-Ambari.md#run-ambari-security-wizard)

---------------
  
### Ambari 2.0 sandbox
- Official HDP 2.2.4 sandbox with Ambari 2.0 is available for download [here](http://hortonworks.com/products/hortonworks-sandbox/#install). It includes
	- Pre-installed Spark 1.2.1
	- Pre-installed views

- ~~Prebuilt sandbox VM with Ambari 2.0 TP with contributed views installed~~

  - ~~Download [here](https://www.dropbox.com/s/filhqw11psth6tq/Hortonworks_2.2_Ambari2.0.ova?dl=0)~~

  - ~~Note to fix the Hive view, you will need to make the below update to the view setting:~~
    - ~~Start Ambari~~
    - ~~admin~~
    - ~~Manage Ambari~~
    - ~~Views~~
    - ~~select Hive~~
    - ~~scroll to bottom~~
    - ~~edit~~
    - ~~Change hive.auth to auth=NONE;user=hive~~


       

### Views screenshots

- Screenshots of [contributed views](https://github.com/apache/ambari/tree/trunk/contrib/views)

---------------------

#### [Hive view](https://github.com/apache/ambari/tree/trunk/contrib/views/hive)

![Image](../master/screenshots/hive-view.png?raw=true)

![Image](../master/screenshots/hive-view-tez.png?raw=true)

---------------------

#### [Capacity scheduler view](https://github.com/apache/ambari/tree/trunk/contrib/views/capacity-scheduler)

![Image](../master/screenshots/Capacity-scheduler-view.png?raw=true)

---------------------

#### [Files view](https://github.com/apache/ambari/tree/trunk/contrib/views/files)

![Image](../master/screenshots/Files-view.png?raw=true)


---------------------

#### [Jobs view](https://github.com/apache/ambari/tree/trunk/contrib/views/jobs)

![Image](../master/screenshots/Jobs-view.png?raw=true)

![Image](../master/screenshots/Jobs-view2.png?raw=true)

---------------------

#### [Tez view](https://github.com/apache/ambari/tree/trunk/contrib/views/tez)

![Image](../master/screenshots/Tez-view.png?raw=true)

![Image](../master/screenshots/Tez-view2.png?raw=true)

---------------------

#### [Slider view](https://github.com/apache/ambari/tree/trunk/contrib/views/slider)

![Image](../master/screenshots/slider-view.png?raw=true)


---------------------

#### [Pig view](https://github.com/apache/ambari/tree/trunk/contrib/views/pig)

![Image](../master/screenshots/pig-view1.png?raw=true)
![Image](../master/screenshots/pig-view2.png?raw=true)


### Setup instructions for contributed views

###### Option 1: Pull the latest view vide, compile and deploy

[update 2/27]: Note per latest from Jeff, to compile views it is no longer needed to have ambari-views.jar in your local maven as ambari-views.jar and the contrib view jars all published to maven

```
#install maven
mkdir /usr/share/maven
cd /usr/share/maven
wget http://mirrors.koehn.com/apache/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz
tar xvzf apache-maven-3.2.5-bin.tar.gz
ln -s /usr/share/maven/apache-maven-3.2.5/ /usr/share/maven/latest
echo 'M2_HOME=/usr/share/maven/latest' >> ~/.bashrc
echo 'M2=$M2_HOME/bin' >> ~/.bashrc
echo 'PATH=$PATH:$M2' >> ~/.bashrc
export M2_HOME=/usr/share/maven/latest
export M2=$M2_HOME/bin
export PATH=$PATH:$M2

#pull code
cd
git clone https://github.com/apache/ambari.git
cd ambari/contrib/views
#No longer needed - tell maven to compile against ambari jar (double check that the jar exists in this location, first)
#mvn install:install-file -Dfile=/usr/lib/ambari-server/ambari-views-1.7.0.169.jar -DgroupId=org.apache.ambari -DartifactId=ambari-views -Dversion=1.3.0-SNAPSHOT -Dpackaging=jar

#Compile view
mvn clean package

#move jars to Ambari dir
cp target/*.jar /var/lib/ambari-server/resources/views

service ambari restart

```

###### Option 2: Deploy views using pre-built jar files

Prebuilt jars are available at https://repository.apache.org/#nexus-search;quick~ambari
```
cd /var/lib/ambari-server/resources/views


wget http://dev.hortonworks.com.s3.amazonaws.com/HDP-LABS/Projects/Ambari/2.0.0-Preview/contrib/views/capacity-scheduler-0.3.0-SNAPSHOT.jar
wget http://dev.hortonworks.com.s3.amazonaws.com/HDP-LABS/Projects/Ambari/2.0.0-Preview/contrib/views/files-0.1.0-SNAPSHOT.jar
wget http://dev.hortonworks.com.s3.amazonaws.com/HDP-LABS/Projects/Ambari/2.0.0-Preview/contrib/views/pig-0.1.0-SNAPSHOT.jar
wget http://dev.hortonworks.com.s3.amazonaws.com/HDP-LABS/Projects/Ambari/2.0.0-Preview/contrib/views/hive-0.1.0-SNAPSHOT.jar

wget https://dl.dropboxusercontent.com/u/114020/views/jobs-1.3.0-SNAPSHOT.jar
wget https://dl.dropboxusercontent.com/u/114020/views/tez-ambari-view-0.6.0-SNAPSHOT.jar


#on non-sandbox
service ambari-server restart
#on sandbox
service ambari restart
```

- Once deployed, create an instance of the view in Ambari
  - http://sandbox.hortonworks.com:8080 > admin > Manage Ambari > Views > (select view) > Create instance > fill out required fields and save
  - To see details of what to fill out in each field, you can refer to the views README on [git](https://github.com/apache/ambari/tree/trunk/contrib/views) or in [TP instructions](https://docs.google.com/a/hortonworks.com/document/d/1u6QPWLOd9Wsd_hp5iNkg0D2xpmylMia7fXpmE3iGL-0/edit#)
  - Now the view should appear in your views area (which you can access via the square icon next to "admin" drop down on upper left)"