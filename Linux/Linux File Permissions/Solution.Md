The Nautilus security team performed an audit on all servers present in Stratos DC. During the audit some critical data/files were identified which were having the wrong permissions as per security standards. Once the report was shared with the production support team, they started fixing the issues one by one. It has been identified that one of the files named /etc/hostname on Nautilus App 2 server has wrong permissions, so that needs to be fixed and the correct ACLs needs to be set.
1. The user owner and group owner of the file should be root user.

2. Others must have read only permissions on the file.

3. User ammar must not have any permission on the file.

4. User jerome should have read only permission on the file.

```
 sudo  setfacl -m u:ammar:--- /etc/hostname 
 sudo  setfacl -m u:jerome:r-- /etc/hostname 
```