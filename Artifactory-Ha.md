##Artifactory HA Installation Guide for DC/OS

##### Architecture of Artifactory HA

![HA Artifactory Architecture](images/HA_Diagram.png)

## To Set Up Artifactory HA in DCOS following are prerequisites:
1. **NFS Storage**
2. **Database (MySQL, Oracle,  MS SQL and PostgreSQL)**
3. **Artifactory Pro Enterprise Value Pack**


## Steps to Set Up Artifactory HA:

1. Add fork of Universe to DC/OS<br />
   ```dcos package repo add JFrog https://github.com/jainishshah17/universe/archive/version-2.x.zip```

2. Mount NFS Storage to Each Private Node of DC/OS Cluster.<br />
    For example: You have artifactoryha.mount.com:/artifactory as your mount point.
    Mount it to /var/data/artha dir of your each private node of DC/OS.<br />
    ```sudo mount artifactoryha.mount.com:/artifactory /var/data/artha```<br />
    All the nodes should share the same file storage, for now the only way is to use NFS. This requirement will be removed in the future.<br />
    Note: Provide permission to write and create subdirectories to /var/data/artha.

3. Install MySQL in DC/OS using Marathon.<br />
    ```dcos marathon app add artifactory-mysql.json```<br />
    The database is used by all the nodes to store metadata attached to artifacts.<br />
	Ex. [artifactory-mysql.json](https://github.com/JFrogDev/artifactory-mesos/blob/master/artifactory-mysql.json)

4. Install artifactory-primary using DC/OS user interface / CLI.<br />
    ```dcos package install artifactory-primary --option=artifactory-primary.json```<br />
    Provide following Values:<br />
    cluster-Home : /var/data/artha {NFS Mount path}<br />
    databse-connection-string : jdbc:mysql://artifactory-mysql.marathon.mesos:3306/artdb?characterEncoding=UTF-8&elideSetAutoCommits=true <br />
    databse-user : root {Database User}<br />
    databse-password : password {Database Password}<br />
    artifactory-licenses: { n Licenses for Artifactory comma separated} <br />

5. Install Artifactory-secondary:DC/OS user interface / CLI.<br />
    ```dcos package install artifactory-secondary --option=artifactory-secondary.json```<br />
   Provide following Values:<br />
   cluster-Home : /var/data/artha {NFS Mount path}<br />
   api-key : API Key of Artifactory generated  by Artifactory-Primary to fech license from Artifactory-Primary (Optional)

6. Install Nginx (Artifactory LB) using Marathon<br />
    ```dcos marathon app add artifactory-nginx.json```<br />
    Ex. [artifactory-nginx.json](https://github.com/JFrogDev/artifactory-mesos/blob/master/artifactory-nginx.json)


7. Go to your DC/OS Public Slave LB and change its Health Check to HTTP:9090/health {Protocol:Port/Path}



### Now try to access your DC/OS Public Slave load balancer you should be able to access Artifactory.

##To use JFrog Artifactory please visit wiki.jfrog.com

