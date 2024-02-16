# Stack Exchange Question 412204

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/412204/make-a-universally-not-required-field-required-using-dynamic-forms-for-flow/417349#417349)

## Answer

One way to enforce a required field is to manually create the field on the screen flow and map it to the record's field and update the record. 

I created a MWE screen flow to show this. I added a screen element where the Opportunity Name is displayed (which is required on the field level) as well as the Description field (which is not required on the field level). 

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/412204/images/Required%20Description%20field.png)

I added a Long Text component that can also be the Description field, but I made it required.

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/412204/images/Optional%20Description%20field.png)

After the screen element, I used an Assign element to map the Long Text component value to the Description field of the Opportunity record variable.

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/412204/images/Map%20screen%20inputs.png)

Lastly, I updated the Opportunity record with the updated record variable.

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/412204/images/Update%20Record.png)

For picklists this method might be more cumbersome as you lose the functionality of displaying picklist values based off of record type. I would then use the decision split as you mentioned because it is less effort to implement.

Good luck!