After doing some security audits of servers, xFusionCorp Industries security team has implemented some new security policies. One of them is to disable direct root login through SSH.
Disable direct SSH root login on all app servers in Stratos Datacenter.
ssh to the all three app servers and open sshd_config file, change ```permitrootlogin``` to no in ```sshd_config``` file, save and close the file and restart sshd service.

```
sudo vi /etc/ssh/sshd_config 
sudo systemctl restart sshd
```