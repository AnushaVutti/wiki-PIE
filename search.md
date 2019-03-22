#Search uses external or hypothetical database for response to search request. The Collection's name is Policy whose documents consists features of policies with their types. The results are displayed using cards. The data model is done this way. 

Policy
{ policyId: Number, policyName: String,members:String,companyName:String, sumInsured: Number, cashlessHospitals: Number, monthlyPremium: Number, yearlyPremium: Number, diseasesCovered: <Disease>, minAge: Number, maxAge: Number,
waitingPeriod: Number, createdAt: TimeStamp, updatedAt: TimeStamp, createdBy: String, updatedBy: String}

#We need disease array to define diseases covered, So we create a separate document for it.

Disease
{ diseaseName: String}

#Documentation for user story
User_story - search service

Http request
{
policyName: String,
disease: String,
insurerName: String,
age: Number
}


HTTP response
{
policyId: Number,
policyName: String,
policyType: String,
insurerName: String,
waitingPeriod: Number,
diseasesCovered: <Disease>,
monthlyPremium: Number,
sumInsured: Number,
minAge: Number,
maxAge: Number
}


Persistent Data Model // This internal database Model is stored as search occurs and this can be used for recommendation.
{
searchValue: String,
count: Number
}

PMB
{
policyId: Number,
policyName: String,
members: String,
insurerName: String,
waitingPeriod: Number,
diseasesCovered: String,
monthlyPremium: Number,
sumInsured: Number,
minAge: Number,
maxAge: Number
}

CMB
{
policyId: Number,
policyName: String,
members: String,
insurerName: String,
waitingPeriod: Number,
diseasesCovered: String,
monthlyPremium: Number,
sumInsured: Number,
minAge: Number,
maxAge: Number
}
Communication Links - userService
