The deployment name is nginx-phpfpm-dp and service name is nginx-service. Figure out the issues and fix them. 

FYI Nginx is configured to use default http port, node port is 30008 and copy index.php under /tmp/index.php to deployment under /var/www/html. Please do not try to delete/modify any other existing components like deployment name, service name etc.

Check the on which port and targetport service is running and change it to 80

``` kubectl edit svc nginx-service ```

Edit the config map nginx-config and add index.php

``` kubectl edit cm nginx-config ```

Restart the deployment (not recommended at all times)

``` kubectl rollout restart deployment <deploymentname> ```

Copy index.php to nginx-container

``` kubectl cp /tmp/index.php <podname>:/var/www/html ```