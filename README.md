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
