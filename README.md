# Cloudant

If you already have an IBM account, you can create cloudant service. I launched the `lite` service. You need to initiate the instance and create credentials in `Credential Services`. Once you're done with that, you can look up the username, password and API key. 

I removed some keys. Cloudant API key and Softlayer API key are different. In `view credentials`,
```
{
  "apikey": "CLOUDANT_APIKEY",
  "host": "xxxxx-bluemix.cloudant.com",
  "iam_apikey_description": "Auto generated apikey during resource-key operation for Instance - crn:v1:bluemix:public:cloudantnosqldb:us-east:a/xxxxxxx:xxxxxxxxx::",
  "iam_apikey_name": "auto-generated-apikey-xxx",
  "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Manager",
  "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/xxx::serviceid:ServiceId-xxxxx",
  "password": "xxxxxxxxxxxxxxxxxxxxxx",
  "port": 443,
  "url": "https://xxxxx-bluemix:xxxxxxxxxx@xxxxx-bluemix.cloudant.com",
  "username": "xxxxx-bluemix"
}
```

You need the `Authorization: BASIC` output from the CLI. So go to your terminal and use the command 
```
$ curl –v –u <account> 'https://<account>.cloudant.com'
```
This is how it will look like, it will ask you `Enter host password for user xxxxx-bluemix`. You need the password from `Credential Servivces` above. 
```
$ curl -v -u xxxxx-bluemix 'https://xxxxx-bluemix.cloudant.com'

Enter host password for user xxxxx-bluemix: 

* Rebuilt URL to: https://xxxxx-bluemix.cloudant.com/
*   Trying 169.60.126.135...
...
...
GET / HTTP/1.1
> Host: db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix.cloudant.com
> Authorization: Basic xxxxxxxxxc5NmFlNQ==
> User-Agent: curl/7.58.0
> Accept: */*
...
...
{"couchdb":"Welcome","version":"2.1.1","vendor":{"name":"IBM Cloudant","version":"7205","variant":"paas"},"features":["geo","scheduler","iam"]}
* Connection #0 to host db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix.cloudant.com left intact
```




