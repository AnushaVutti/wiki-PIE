### Company Login

## Description
On clicking the hyperlink "ARE YOU A INSURANCE PROVIDER?" it will redirect to the company login/register page. On the left side of the screen , we will have fields for registering as a new insurance company and on the right side of the screen , we will have the fields for login. 

**For logging in we have to fill the following fields**
"Enter your CompanyEmail/licenseNumber": ,
"Enter your password" : 

**Persistence Data Model**
{

 "licenseNumber": string,
 
 "password" : string (hashed)

}

**Message Bus Producing**
Null

**Consuming Message Bus**
{

 "licenseNumber": ,

 "password" :
 
}
