# Company Registration

## Description
On clicking the hyperlink _"ARE YOU A INSURANCE PROVIDER?"_ it will redirect to the company login/register page.
On the left side of the screen , we will have fields for registering as a new insurance company and on the right side of the screen , we will have the fields for login.

**For registering we have to fill the following fields**

 "licenseNumber" : ,

 "companyName" : ,

 "companyEmail" : ,

 "companyPhoneNumber": ,

 "companyAddress" : ,

 "password" : ,

 "securityQuestion" : ,

 "securityAnswer" : 



**Persistence Data Model**
{

 "_id" : "number",

 "licenseNumber" : string ,

 "companyName" : string ,

 "companyEmail" : string ,

 "companyPhoneNumber": string ,

 "companyAddress" : string ,

 "password" : string ,

 "securityQuestion" : string ,

 "securityAnswer" : string,

 "createAt" : timestamp,

 "lastUpdated" : timestamp

}

**Message Bus Producing**

{

 "_id" : "number",

 "licenseNumber" : string ,

 "companyName" : string ,

 "companyEmail" : string ,

 "companyPhoneNumber": string ,

 "companyAddress" : string ,

 "password" : string ,

 "securityQuestion" : string ,

 "securityAnswer" : string

}

**Consuming Message Bus**

{

 "_id" : "number",

 "licenseNumber" : string ,

 "companyName" : string ,

 "companyEmail" : string ,

 "companyPhoneNumber": string ,

 "companyAddress" : string ,

 "password" : string ,

 "securityQuestion" : string ,

 "securityAnswer" : string
}
