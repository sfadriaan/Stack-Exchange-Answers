# Stack Exchange Question 416744

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/417558/set-a-custom-checkbox-field-to-true-based-on-another-checkbox-field-value-and-a)

## Answer

You basically already wrote the formula down in words.

Create the `Is_International_Student__c` field as a boolean formula field.

Then add the formula:
```
AND(Is_Student__c==TRUE,
    CONTAINS(Dental_School__c,'Mexico')
)
```

If `Dental_School__c` needs to start with "Mexico", then you can update the formula to:
```
AND(Is_Student__c==TRUE,
    LEFT(Dental_School__c,6)=='Mexico'
)
```

Good luck!