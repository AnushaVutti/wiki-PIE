# 1.Persistant Data Model

1a)Policy
{  policyId: Number,
   policyName: String,
   insurerName: String,
   member:String, 
   sumInsured: Number, 
   numberOfCashLessHospitals: Number,
   cashLessHospitals:[Hostipal],   
   monthlyPremium: Number, 
   yearlyPremium: Number, 
   diseasesCovered: [Disease]* 1. # ## ### , 
   minAge: Number,
   maxAge: Number,
   waitingPeriod: Number, 
   createdAt: TimeStamp,
   updatedAt: TimeStamp, 
   createdBy: String,
   updatedBy: String
}

1a)Disease
{
diseaseName:String
}
1a)Hospital
{
hospitalName:String;
}

2a)GET Request

http://localhost:8080/api/v1/insurer/myPolicies

2a)GET Response

{  "policyId": 1, 
   "policyName": "Cancer_safe",
   "insurerName":"Maxbupa",
   "member":"self", 
   "sumInsured": "5000", 
   "numberOfCashLessHospitals": 2,
   "cashLessHospitals":["appolo","munich"],  
   "monthlyPremium": "5433", 
   "yearlyPremium": "60000", 
   diseasesCovered: ["cancer","accident"], 
   minAge: "25",
   maxAge: "60",
   waitingPeriod: 3, 
   createdAt: today,
   updatedAt: today, 
   createdBy: "maxbupa",
   updatedBy: "maxbupa"
}


2b)POST Request
http://localhost:8080/api/v1/insurer/addPolicy
Body

{  "policyId": 1, 
   "policyName": "Cancer_safe",
   "insurerName":"Maxbupa",
   "member":"self", 
   "sumInsured": "5000", 
   "numberOfCashLessHospitals": 2,
   "cashLessHospitals":["appolo","munich"],
   "monthlyPremium": "5433", 
   "yearlyPremium": "60000", 
   diseasesCovered: ["cancer","accident"], 
   minAge: "25",
   maxAge: "60",
   waitingPeriod: 3, 
   createdAt: today,
   updatedAt: today, 
   createdBy: "maxbupa",
   updatedBy: "maxbupa"
}


2b)POST Response

{  "policyId": 1, 
   "policyName": "Cancer_safe",
   "insurerName":"Maxbupa",
   "member":"self", 
   "sumInsured": "5000", 
   "numberOfCashLessHospitals": 2,
   "cashLessHospitals":["appolo","munich"],
   "monthlyPremium": "5433", 
   "yearlyPremium": "60000", 
   diseasesCovered: ["cancer","accident"], 
   minAge: "25",
   maxAge: "60",
   waitingPeriod: 3, 
   createdAt: today,
   updatedAt: today, 
   createdBy: "maxbupa",
   updatedBy: "maxbupa"
}


3.Message Bus Publishing
{
   "policyId": 1, 
   "policyName": "Cancer_safe",
   "insurerName":"Maxbupa",
   "member":"self", 
   "sumInsured": "5000", 
   "numberOfCashLessHospitals": 2,
   "cashLessHospitals":["appolo","munich"],
   "monthlyPremium": "5433", 
   "yearlyPremium": "60000", 
   diseasesCovered: ["cancer","accident"], 
   minAge: "25",
   maxAge: "60",
   waitingPeriod: 3, 
   createdAt: today,
   updatedAt: today, 
   createdBy: "maxbupa",
   updatedBy: "maxbupa"
}

4.Consuming Message Bus
Null


