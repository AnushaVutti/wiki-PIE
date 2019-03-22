1. Performance in recomandation and mypolicy should be improved.

2. Buy option and logic needs to be implimented: things needs to be updated after buying: <br/>
   ->Recomandation: It should update policy node with new insured<br/>
   ->Insurer: after buying we need to add the insured details to Insured's database.<br/>
   ->Insured: after buying we need to add the policy to policy list of insured.<br/>

3. Whenever any new user get register at the same time it should go to external DB and fetch the list of policies 
   and save it to insured's DB.

4. When insured port to some other policy he should update the policy list of his own and at the same time insured 
   list of insurer(both privious and new insurer) should be updated.

5. HttpStatus code should be given as 200(OK) in order to pass the object to front-end.

6. For the MatDialog to pop up the new component,the component which should be shown in the pop up , should be added in the entryComponents in the app.module.ts



 

