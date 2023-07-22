The Nautilus DevOps team is planning to set up a Nagios monitoring tool to monitor some applications, services etc. They are planning to deploy it on Kubernetes cluster. Below you can find more details.
1) Create a deployment nagios-deployment for Nagios core. The container name must be nagios-container and it must use jasonrivers/nagios image.
2) Create a user and password for the Nagios core web interface, user must be xFusionCorp and password must be LQfKeWWxWD. (you can manually perform this step after deployment)
3) Create a service nagios-service for Nagios, which must be of targetPort type. nodePort must be 30008.
You can use any labels as per your choice.
Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.

Create a yaml file and paste below code.

```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nagios-deployment
  labels:
    app: nagios
spec:
  selector:
    matchLabels:
      app: nagios
  template:
    metadata:
      labels:
        app: nagios
    spec:
      containers:
      - name: nagios-container
        image: jasonrivers/nagios
        ports:
        -  containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nagios-service
spec:
  type: NodePort
  selector:
    app: nagios
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```
Save and close the file and apply the config, once done, verify the deployment by opening the port. After validation execute below commands.


```
kubectl exec -it <podname> -- /bin/bash
```

After entering into the pod run below command and enter the password.

```
htpasswd /opt/nagios/etc/htpasswd.users <Given user name>

```