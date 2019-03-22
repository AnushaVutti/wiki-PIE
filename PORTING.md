In user dashboard, on clicking Porting Request, a porting form will be displayed. User will fill the form and submit it. Upon submission, the notification mail will be sent to old insurer and form will go to the new insurer and the new insurer will send the response within 15 days.
# HTTP Request:
{
"_id" :integer, "userName" :string, "age" :integer, "existingInsuranceCompany" :string, "existingPolicyId" : integer, "existingPolicyName" :string, "newInsuranceCompany" :string, "newPolicyName" :string, "diseases" :string[], "remainingWaitingPeriodForDiseases" :integer, "familyMembers" :integer, formStatus" :string }


# HTTP Response:
{"_id" :integer, "userName" :string, "age" :integer, "existingInsuranceCompany" :string, "existingPolicyId" : integer, "existingPolicyName" :string, "newInsuranceCompany" :string, "newPolicyName" :string, "diseases" :string[], "remainingWaitingPeriodForDiseases" :integer}


# Persistence Data Model:
{"requestId" :integer, "requestStatus" :string, "newInsuranceCompany" :string, "newPolicyName" :string}


# Producing Message Bus:
{"_id" :integer, "userName" :string, "age" :integer, "existingInsuranceCompany" :string, "existingPolicyId" : integer, "existingPolicyName" :string, "requestId" :integer, "requestStatus" :string, "newInsuranceCompany" :string, "newPolicyName" :string, "diseases" :string[], "familyMembers" :integer, "remainingWaitingPeriodForDiseases" :integer }


# Consuming Message Bus:
{"_id" :integer, "userName" :string, "age" :integer, "existingInsuranceCompany" :string, "existingPolicyId" : integer, "existingPolicyName" :string, "newInsuranceCompany" :string, "newPolicyName" :string, "diseases" :string[], "remainingWaitingPeriodForDiseases" :integer, "formStatus" :string}


