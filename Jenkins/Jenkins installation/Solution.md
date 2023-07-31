
The DevOps team of xFusionCorp Industries is planning to setup some CI/CD pipelines. After several meetings they have decided to use Jenkins server. So, we need to setup a Jenkins Server as soon as possible. Please complete the task as per requirements mentioned below:

1. Install jenkins on jenkins server using yum utility only, and start its service. You might face timeout issue while starting the Jenkins service, please refer this link for help.

2. Jenkin's admin user name should be theadmin, password should be Adm!n321, full name should be Javed and email should be javed@jenkins.stratos.xfusioncorp.com.

Note:
1. For this task ssh into jenkins server using user root and password S3curePass from jump host.

2. To complete the jenkins installation after installing packages and after starting the jenkins service, click on the Jenkins button on the top bar.

Perform These steps inside the jenkins server

```
yum install wget -y
sudo wget -O /etc/yum.repos.d/jenkins.repo     https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
sudo yum install java-17-openjdk
sudo yum install jenkins
sudo systemctl daemon-reload
systemctl enable jenkins
systemctl start jenkins
systemctl statusjenkins
systemctl status jenkins
```

Once the jenkins service is up open jenkins, by clicking on the button at top right.
Perform below step in jenkins server, copy and paste the password in the placeholder.
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
Then install the plugins, after plugins installation is done, enter the user details as specified in the task.
