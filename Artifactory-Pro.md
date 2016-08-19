##Artifactory-Pro Installation Guide for DC/OS

## To Set Up Artifactory HA in DC/OS following are prerequisites:
1. **Database (MySQL)**
2. **Artifactory Pro License**

*[Here is guide to install MySQL in DC/OS](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/install-mysql.md)

*[Go here to Get your Trial License](https://www.jfrog.com/artifactory/free-trial-mesosphere/)

*Steps to Install Artifactory Pro

1. Select Artifactory Package from Universe

![Artifactory Package in Universe](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Universe_Artifactory.png)

2. Click on Install-> Advance Installation-> Pro

3. Provide license and database details as shown in screen shot
![Artifactory Advance installation Option](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/ArtifactoryPro_Install_Option.png)

NOTE: Make sure database name, is correct in connection-string as well as username & password for database.

4. Install Artifactory-Pro by clicking on Review and Install button.

5. Make sure Artifactory is running and its healthy by looking at Marathon UI.
![Artifactory Health in Marathon UI](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Artifactory_Health.png)

##NOW you are just one step away in accessing Artifactory

5. [Install Artifactory-lb by following this guide] (https://github.com/JFrogDev/artifactory-dcos/blob/master/install-artifactory-lb.md)
