# **RECOMMENDATIONS**

The Recommendation Service uses neo4j database to recommend policies to the policy holder based on his profile.The Recommendation Service interacts with the Policy holder service to get the details of the policy holder to recommend services. The Recommendation service interacts with the Insurance Company to add new policies and companies registered to the neo4j database.

## Recommendations system :
For a user(insured), the system should recommend:
* polcies based on the number of views(similar policies)
* policies bases on existing illness, age and gender
* policies bases on existing illness and age
* policies bases on existing illness and gender
* policies bases on existing age and gender
* similar policies with the existing insurer(the user shouldn't hold similar/same policies )(this applies to all recommendations)
* all above recommendations should apply to insured dependants




 ## HTTP Request:
{ "user_id": integer,"policy_id":integer,"company_id":integer,"age":integer,"location":string
}

## HTTP Response:
{ "company_name":string,"policy_name":string,"min_age":integer,"max_age":integer,"sum-insured":integer,"premium":integer,"policy_term":integer
}

## Data Persistence Model
The Recommendation Service uses neo4j database.The nodes are as follows:
* Insurer
* Policy
* User or policy holder
* Disease


## Message Bus Providing(MBP):
{ "company_name":string,"policy_name":string,"min_age":integer,"max_age":integer,"sum-insured":integer,"premium":integer,"policy_term":integer
}

## Consuming Message Bus(CMB):
The Recommendation Service consumes information from Policy holder Dashboard and Insurance Company Dashboard.The Policy holder Dashboard provides all the information regarding the policy holder.The Insurance Company dashboard will provide the information with respect to the new policies added.

### Policy holder Dashboard's information consumed:
{
"user_id":integer,"user_name":"string",age":integer,"disease":string,"gender":string,"family_Members":integer
}

### Insurance Company Dashboard's information consumed:
{
"company_id":integer,"company_name":string
}
{
"diseases_Covered":string,
  "policy_Id":number,
  "policy_Name": string,
  "max_Age": number,
  "insurer_Name":string,
  "min_Age":number
}
