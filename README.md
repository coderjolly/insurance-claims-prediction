# Insurance Claims Prediction

We sell automobile insurance policies where customers pay us an annual premium to insure their vehicle for a year. Assume that each customer only has one vehicle, and one vehicle only has one driver (i.e., the customer). Also assume that if they get into an accident, they will always open a claim with us.

#### Input
In the attached dataset, you will see the following fields:
-	Claim ID: customer unique ID
-	Gender: gender of customer
-	Age: age of the customer at the time of policy submission
-	Driving license: valid driver's license at the time of policy submission (1 = has a driving license, 0 = no driving license)
-	Region code: region code of the customer’s address
-	Previously insured: customer is previously insured with Northbridge (1 = yes, previously insured with Northbridge, 0 = no, not previously insured with Northbridge)
-	Vehicle age: age of the customer’s vehicle at the time of policy submission
-	Previous_Vehicle_Damage: customer’s vehicle has previous damage (1 = has previous damage, 0 = no previous damage)
-	Annual premium: annual premium that the customer pays for their automobile policy
-	Policy_Sales_Channel: encoded sales channel that customer use to purchase their policy
-	Response: whether customer submitted a claim (1 = submitted claim, 0 = did not submit claim)

#### Objective
The task is to create a model that predicts whether a customer will get into an accident and submit a claim.
