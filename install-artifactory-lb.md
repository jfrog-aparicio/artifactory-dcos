##Artifactory-lb Installation Guide for DC/OS

## To Set Up Artifactory-lb in DC/OS following are prerequisites:
1. **Running Artifactory**

## Steps to install Artifactory-lb:

1. Select Artifactory-lb package from Universe.
![Artifactory-lb Package in Universe](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Universe_Artifactory-lb.png)

2. Click on Install -> Advance Installation -> artifactory.

3. Go to your Mesos UI.
![Mesos UI](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Mesos.png)

4. Select Artifactory -> Artifactory-logs 
![Artifactory Logs directory](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Artifactory_Logs_Dir.png)

5. Select artifactory.log file and you will see output as following. Copy API key from artifactory.log file as showed in screen shot.
![Artifactory API Key](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Artifactory_Log.png)

6. Paste selected API key in Artifactory-lb advance installation as follows. Then review and install.
![Artifactory Advance Installation](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Artifactory-lb_Install_Options.png)


7. Make sure Artifactory-lb is running and its healthy by looking at Marathon UI.
![Artifactory-lb Health in Marathon UI](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Artifactory-lb_Health.png)

### Awesome!! now you can access artifactory UI by going to public ip of node where Artifactory-lb is running.

Here is how Artifactory UI looks like!!!
![Artifactory UI](https://raw.githubusercontent.com/JFrogDev/artifactory-dcos/master/images/Artifactory_UI.png)