# Artifactory HA setup in DC/OS

##Artifactory HA Installation Guide for DC/OS

##### Architecture of Artifactory HA

![HA Artifactory Architecture](https://raw.githubusercontent.com/jainishshah17/Images/master/artifactory%20diagram_landscape_green.jpg)

## To Set Up Artifactory HA in DCOS following are prerequisites:
1. **NFS Storage**
2. **Database (MySQL, Oracle,  MS SQL and PostgreSQL)**
3. **Artifactory Pro Enterprise Value Pack**
4. **Load Balancer With Sticky Session**

## Steps to Set Up Artifactory HA:

1. Add fork of Universe to DC/OS
   ```dcos package repo add JFrog https://github.com/jainishshah17/universe/archive/version-2.x.zip```

2. Mount NFS Storage to Each Private Node of DC/OS Cluster.
    For example: You have artifactoryha.mount.com:/artifactory as your mount point.
    Mount it to /var/data/artha dir of your each private node of DC/OS.
    ```sudo mount artifactoryha.mount.com:/artifactory /var/data/artha```
    Note: Provide permission to write and create subdirectories to /var/data/artha.

3. Install MySQL in DC/OS using Marathon.
    ```dcos marathon app add mysql.json```
	Ex. [mysql.json](https://github.com/JFrogDev/artifactory-mesos/blob/master/mysql.json)
	
4. Install artifactory-primary using DC/OS user interface / CLI.
    ```dcos package install artifactory-primary --option=artifactory-primary.json```
    Provide following Values:
    Cluster-Home : /var/data/artha {NFS Mount path}
    Connection-string : jdbc:mysql://mysql.marathon.mesos:3306/artdb?characterEncoding=UTF-8&elideSetAutoCommits=true 
    user : root {Database User}
    password : password {Database Password}
    Artifactory-licenses: { n Licenses for Artifactory comma separated} 

5. Install Artifactory-secondary:DC/OS user interface / CLI.
    ```dcos package install artifactory-secondary --option=artifactory-secondary.json```
   Provide following Values:
   Cluster-Home : /var/data/artha {NFS Mount path}
   api-key : API Key of Artifactory generated  by Artifactory-Primary to fech license from Artifactory-Primary

6. Install Nginx (Artifactory LB) using Marathon
    ```dcos marathon app add nginx.json```
    Ex. [nginx.json](https://github.com/JFrogDev/artifactory-mesos/blob/master/nginx-artifactory.json)


7. Go to your DC/OS Public Slave LB and change its Health Check to HTTP:9090/health {Protocol:Port/Path} 



### Now try to access your DC/OS Public Slave load balancer you should be able to access Artifactory.




