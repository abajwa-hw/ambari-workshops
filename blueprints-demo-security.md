- ensure hosts file contains all cluster hosts
cat /etc/hosts

- on node1 run pre-reqs and install/start ambari-server
export install_ambari_agent=true
export install_ambari_server=true
export ambari_version=2.0.0
curl -sSL https://raw.githubusercontent.com/seanorama/ambari-bootstrap/master/ambari-bootstrap.sh | sudo -E sh

- on node2-4 run pre-reqs and install.start ambari-agents
export ambari_server=node1
curl -sSL https://raw.githubusercontent.com/seanorama/ambari-bootstrap/master/ambari-bootstrap.sh | sudo -E sh

-  remaining steps on Ambari server node

- install folder for custom services
yum install -y git

- For security
cd /var/lib/ambari-server/resources/stacks/HDP/2.2/services
git clone https://github.com/abajwa-hw/openldap-stack.git   
git clone https://github.com/abajwa-hw/nslcd-stack.git  
git clone https://github.com/abajwa-hw/kdc-stack.git    

- download and unzip JCE - prereq for kerborizing cluster - http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html
unzip -o -j -q /root/scripts/UnlimitedJCEPolicyJDK7.zip -d /usr/lib/jvm/jre-1.7.0-openjdk.x86_64/lib/security/
#unzip -o -j -q /var/lib/ambari-server/resources/UnlimitedJCEPolicyJDK7.zip -d /usr/jdk64/jdk1.7.0_67/jre/lib/security/

- For datascience
cd /var/lib/ambari-server/resources/stacks/HDP/2.2/services
git clone https://github.com/randerzander/r-service
git clone https://github.com/randerzander/jupyter-service
git clone https://github.com/abajwa-hw/zeppelin-stack.git   

cd

- Optional: if component has start dependencies on others, then add here:
vi /var/lib/ambari-server/resources/stacks/HDP/2.2/role_command_order.json



- restart Ambari
service ambari-server restart
service ambari-agent restart

-  <Optional> - If you don't have a blueprint, you can generate BP and cluster file using Ambari recommendations
# see https://github.com/seanorama/ambari-bootstrap/tree/master/deploy
yum install -y python-argparse
git clone https://github.com/seanorama/ambari-bootstrap.git

#optional - limit the services for faster deployment
export ambari_services="HDFS MAPREDUCE2 YARN ZOOKEEPER"

export deploy=false
cd ambari-bootstrap/deploy
bash ./deploy-recommended-cluster.bash

cd tmpdir*

#edit the blueprint to add custom COMPONENT names (not service name) e.g. XXX_MASTER
vi blueprint.json

#edit cluster file if needed
vi cluster.json

#</Optional>

- Confirm the Agent hosts are registered with the Server.
curl -u admin:admin -H  X-Requested-By:ambari http://localhost:8080/api/v1/hosts

- ensure agent on ambari node is up
service ambari-agent status

- register BP as securityBP and deploy cluster with name securedCluster
curl -u admin:admin -H  X-Requested-By:ambari http://localhost:8080/api/v1/blueprints/securityBP -d @blueprint-1node-security.json
curl -u admin:admin -H  X-Requested-By:ambari http://localhost:8080/api/v1/clusters/securedCluster -d @cluster-1node.json


- register BP as securityBP and deploy cluster with name securedCluster
curl -u admin:admin -H  X-Requested-By:ambari http://localhost:8080/api/v1/blueprints/securityBP -d @blueprint-4node-security.json
curl -u admin:admin -H  X-Requested-By:ambari http://localhost:8080/api/v1/clusters/securedCluster -d @cluster.json

- register BP as datascienceBP and deploy cluster with name DSCluster
curl -u admin:admin -H  X-Requested-By:ambari http://localhost:8080/api/v1/blueprints/datascienceBP -d @blueprint-4node-datascience.json
curl -u admin:admin -H  X-Requested-By:ambari http://localhost:8080/api/v1/clusters/DSCluster -d @cluster.json


- Optional - Troubleshooting: incase you need to re-run you can delete the cluster and BP
curl -u admin:admin  -H  X-Requested-By:ambari -X DELETE http://localhost:8080/api/v1/clusters/securedCluster
curl -u admin:admin  -H  X-Requested-By:ambari -X DELETE http://localhost:8080/api/v1/blueprints/securityBP
service ambari-agent restart

- Optional - Troubleshooting: check blueprint
curl -u admin:admin  -H  X-Requested-By:ambari  http://localhost:8080/api/v1/blueprints/securityBP

- Optional:check status of cluster creation via REST
curl -u admin:admin http://localhost:8080/api/v1/clusters/mycluster/requests/1

- open ambari UI and monitor install

-  After OpenLDAP, KDC and NSLCD services are up...

- check openldap install
ldapsearch -W -h localhost -D "cn=admin,dc=hortonworks,dc=com" -b "dc=hortonworks,dc=com"
 
- check NSLCD
id ali
groups ali

-  check KDC
kadmin -p admin/admin -w hortonworks -r HORTONWORKS.COM -q "get_principal admin/admin"

-  kinit as admin
kinit admin/admin

-  http://docs.hortonworks.com/HDPDocuments/Ambari-2.0.0.0/Ambari_Doc_Suite/Ambari_Security_v20.pdf

- sync Ambari with LDAP

ambari-server setup-ldap

Using python  /usr/bin/python2.6
Setting up LDAP properties...
Primary URL* {host:port} : sandbox.hortonworks.com:389
Secondary URL {host:port} : sandbox.hortonworks.com:389
Use SSL* [true/false] (false):
User object class* (posixAccount):
User name attribute* (uid):
Group object class* (posixGroup):
Group name attribute* (cn):
Group member attribute* (memberUid):
Distinguished name attribute* (dn):
Base DN* : ou=Users,dc=hortonworks,dc=com
Referral method [follow/ignore] : follow
Bind anonymously* [true/false] (false):
Manager DN* : cn=admin,dc=hortonworks,dc=com
Enter Manager Password* : hortonworks
Re-enter password: hortonworks

ambari-server restart
ambari-server sync-ldap --all

- Login to ambari as ali and notice no views

- Login as admin and add ali as Ambari admin

- now re-try login
 
- start kerberos wizard with below
KDC host: node1
realm name: HORTONWORKS.COM
kadmin host: node1
princ: admin/admin
pass: hortonworks


- to start KDC via API
export SERVICE=KRB5
export PASSWORD=admin
export AMBARI_HOST=localhost
export CLUSTER=securedCluster

- start service
curl -u admin:$PASSWORD -i -H 'X-Requested-By: ambari' -X PUT -d '{"RequestInfo": {"context" :"Start $SERVICE via REST"}, "Body": {"ServiceInfo": {"state": "STARTED"}}}' http://$AMBARI_HOST:8080/api/v1/clusters/$CLUSTER/services/$SERVICE

curl -u admin:$PASSWORD -i -H 'X-Requested-By: ambari' -X GET http://$AMBARI_HOST:8080/api/v1/clusters/$CLUSTER/services/$SERVICE


- test HDFS access with/without kinit
kadmin.local
addprinc ali@HORTONWORKS.COM
#hortonworks
exit

su ali
hadoop fs -ls /
kinit
hadoop fs -ls /


- import data
cd /tmp
wget https://raw.githubusercontent.com/abajwa-hw/security-workshops/master/data/sample_07.csv
wget https://raw.githubusercontent.com/abajwa-hw/security-workshops/master/data/sample_08.csv

kinit -kt /etc/security/keytabs/hive.service.keytab hive/sandbox.hortonworks.com@HORTONWORKS.COM
hive
use default;

CREATE TABLE `sample_07` (
`code` string ,
`description` string ,  
`total_emp` int ,  
`salary` int )
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' STORED AS TextFile;

load data local inpath '/tmp/sample_07.csv' into table sample_07;

CREATE TABLE `sample_08` (
`code` string ,
`description` string ,  
`total_emp` int ,  
`salary` int )
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' STORED AS TextFile;

load data local inpath '/tmp/sample_08.csv' into table sample_08;
exit;

kdestroy

- Rangersetup
# http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.4/Ranger_Install_Over_Ambari_v224/Ranger_Install_Over_Ambari_v224.pdf

- setup existing MySQL for Ranger DB
mysql
select host, user, password from mysql.user;
-- only if this user does not exist create it
create user 'root'@'%' identified by 'hortonworks'; 
grant all privileges on *.* to 'root'@'%' identified by 'hortonworks' with grant option; 
flush privileges;
set password for 'root'@'localhost'=password ('hortonworks');
set password for 'root'@'sandbox.hortonworks.com'=password ('hortonworks');
set password for 'root'@'127.0.0.1'=password ('hortonworks');
exit

- double check login
mysql -u root -phortonworks -h sandbox.hortonworks.com

- enable ambari to recognize mysql jar
ambari-server setup --jdbc-db=mysql --jdbc-driver=/usr/share/java/mysql-connector-java-5.1.17.jar

- copy mysql jar to other nodes (if any)
scp /usr/share/java/mysql-connector-java-5.1.17.jar root@node2:/usr/share/java/
scp /usr/share/java/mysql-connector-java-5.1.17.jar root@node3:/usr/share/java/
scp /usr/share/java/mysql-connector-java-5.1.17.jar root@node4:/usr/share/java/

- Add  service > Ranger > select same host where Mysql is
Ranger DB host: sandbox.hortonworks.com
set passwords to hortonworks
  - Rager settings
    - External URL: http://sandbox.hortonworks.com:6080
	- SYNC_LDAP_BIND_DN: cn=admin,dc=hortonworks,dc=com
	- SYNC_LDAP_BIND_PASSWORD: hortonworks
	- SYNC_LDAP_URL: ldap://sandbox.hortonworks.com:389
	- SYNC_LDAP_USER_NAME_ATTRIBUTE: uid
	- SYNC_LDAP_USER_SEARCH_BASE: ou=Users,dc=hortonworks,dc=com
	- SYNC_LDAP_USER_SEARCH_FILTER : (space)
	- SYNC_SOURCE: ldap

- ####setup HDFS plugin on kerborized setup

- create group admins in Ranger


- add user hdfsuser to Ranger as well with password hortonworks1

- create os user hdfsuser with same password: hortonworks1
adduser hdfsuser 
passwd hdfsuser

- create princpal
kadmin.local -q 'addprinc -pw hdfsuser hdfsuser@HORTONWORKS.COM'

- HDFS configs > Advanced ranger-hdfs-plugin-properties
Enable Ranger for HDFS: true
Ranger repository config user: hdfsuser@HORTONWORKS.COM
Ranger repository config password: hortonworks1
common.name.for.certificate: (space)

- HDFS configs > Custom core-site
hadoop.proxyuser.hive.groups=users, sales, legal, admins
hadoop.proxyuser.hive.hosts=node1,node2,node3,node4

- restart HDFS


- test HDFS audits before and after enabling policy
su ali
hadoop fs -ls /
hadoop fs -ls /tmp/hive


- ####setup Hive plugin on kerborized setup

- create os user hiveuser with same password: hortonworks1
adduser hiveuser 
passwd hiveuser

- create princpal
kadmin.local -q 'addprinc -pw hiveuser hiveuser@HORTONWORKS.COM'

- setup Hive repo per doc
Enable Ranger for HIVE: true
Ranger repository config user: hiveuser@HORTONWORKS.COM
Ranger repository config password: hortonworks1
common.name.for.certificate: 


- create policies that allow read access for sales group
sample_07 partial
sample_08 full


- May need to allow user access on /user HDFS dir
sudo -u hdfs hadoop fs -chmod 777 /user


su ali
klist
kinit
beeline
!connect jdbc:hive2://sandbox.hortonworks.com:10000/default;principal=hive/sandbox.hortonworks.com@HORTONWORKS.COM

!connect jdbc:hive2://localhost:10000/default;principal=hive/node1@HORTONWORKS.COM
