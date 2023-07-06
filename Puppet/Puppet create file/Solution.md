The Puppet master and Puppet agent nodes have been set up by the Nautilus DevOps team so they can perform testing. In Stratos DC all app servers have been configured as Puppet agent nodes. Below are details about the testing scenario they want to proceed with.
Use Puppet file resource and perform the below given task:
Create a Puppet programming file blog.pp under /etc/puppetlabs/code/environments/production/manifests directory on master node i.e Jump Server.
Using /etc/puppetlabs/code/environments/production/manifests/blog.pp create a file blog.txt under /opt/devops directory on App Server 2.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

``` sudo vi /etc/puppetlabs/code/environments/production/manifests/blog.pp  ```

```
class file_create {
file { '/opt/devops/blog.txt':
ensure => present
}
}
node 'target host' {
include file_create
}
```

Run ```puppet agent -t``` on target host.