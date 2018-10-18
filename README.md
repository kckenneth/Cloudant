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

Update your `.bash_profile`
```
$ vi .bash_profile
```
Add the following line at the end with the `Authorization: Basic` you got from the CLI command above. 
```
alias acurl="curl -s --proto '=https' -g -H 'Authorization: Basic <output-of-base64>'"
```
Now open a new terminal or activate the `.bash_profile` by `$ source .bash_profile`. Now you can check your account information by
```
$ acurl -X GET 'https://xxxxx-bluemix.cloudant.com'

{"couchdb":"Welcome","version":"2.1.1","vendor":{"name":"IBM Cloudant","version":"7205","variant":"paas"},"features":["geo","scheduler","iam"]}
```
For some reason, I can still get the cloudant by the following command without setting up all those Authorization: Basic and such. 
```
$ curl -X GET 'https://xxxxx-bluemix.cloudant.com'

{"couchdb":"Welcome","version":"2.1.1","vendor":{"name":"IBM Cloudant","version":"7205","variant":"paas"},"features":["geo","scheduler","iam"]}

$ curl -X GET 'https://xxxxx-bluemix.cloudant.com' | jq .

{
  "couchdb": "Welcome",
  "version": "2.1.1",
  "vendor": {
    "name": "IBM Cloudant",
    "version": "7205",
    "variant": "paas"
  },
  "features": [
    "geo",
    "scheduler",
    "iam"
  ]
}
```

### 1. Create a DB
```
$ curl -X PUT -H 'Content-Type: application/json' https://db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix:password@db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix.cloudant.com/crud/

{"ok":true}
```
### 2. Updating the DB
```
$ curl -d '{"season": "summer", "weather": "usually warm and sunny"}' -X POST https://db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix:password@db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix.cloudant.com/crud/ -H "Content-Type:application/json"

{"ok":true,"id":"ce8a63e4a5665fa4c2c32704f5bb4594","rev":"1-0af5e64fe24d262db237b9f14046f490"}
```
### 3. Checking the DB
```
$ curl https://db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix:password@db5a2375-a143-4e1d-93d2-24a547f075e1-bluemix.cloudant.com/crud/_all_docs

{"total_rows":1,"offset":0,"rows":[
{"id":"ce8a63e4a5665fa4c2c32704f5bb4594","key":"ce8a63e4a5665fa4c2c32704f5bb4594","value":{"rev":"1-0af5e64fe24d262db237b9f14046f490"}}
]}
```


























