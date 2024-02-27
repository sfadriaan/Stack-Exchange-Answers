# Stack Exchange Question 418722

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/418722/formula-to-check-if-field-value-is-changed-and-not-null-in-flow/418754#418754)

## Answer

I was able to reproduce the flow with the information you provided and it did what was required.

1. I used the Account object
2. Triggers on record update
3. When the `PersonMobile` field is changed and not null, update Important Notes (`FinServ__Notes__c`) field with current DateTime:

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/418722/flow-entry-criteria.png)

I tested both scenarios where the mobile phone is changed to something else as well as when the mobile phone is removed and no other value is provided (thus field is `null` and flow should not trigger).

When it comes to using formulas for checking if a field is null/blank, Salesforce gives you [ISBLANK](https://help.salesforce.com/s/articleView?id=sf.customize_functions_isblank.htm&type=5) and [ISNULL](https://help.salesforce.com/s/articleView?id=sf.customize_functions_isnull.htm&type=5), with the preferred one being `ISBLANK` for text fields. 

I sometimes have sporadic success with `ISBLANK` and would rather use something more explicit such as `{!$Record.PersonMobilePhone}<>""` which I have found to be more consistent.

I updated my formula used in the entry criteria of my flow to:

`ISCHANGED({!$Record.PersonMobilePhone}) && {!$Record.PersonMobilePhone}<>""`

and I got the same result. 

Good luck!