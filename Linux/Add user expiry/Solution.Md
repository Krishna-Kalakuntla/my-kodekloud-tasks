A developer named ravi has been assigned Nautilus project temporarily as a backup resource. As a temporary resource for this project, we need a temporary user for ravi. It’s a good idea to create a user with an expiration date so that the user won't be able to access servers beyond that point.

Therefore, create a user named ravi on the App Server 3 in Stratos Datacenter. Set expiry date to 2021-04-15. Make sure the user is created as per standard and is in lowercase.

```
useradd -e 2021-04-15
```