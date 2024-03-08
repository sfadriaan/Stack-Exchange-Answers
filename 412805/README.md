# Stack Exchange Question 412805

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/412805/omnistudiodataraptor-id-of-type-reference-has-invalid-value/419205#419205)

## Answer

I replicated your setup and did not receive any errors. The error might be related to what information you are mapping to the relevant fields.

Here is my DR Load:

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/412805/DR-Load-Objects.png)

I also mapped the required values to the `Account` Object and `Account Contact Relation` Object:

```json
{
  "Account": {
    "LastName": "Van Niekerk"
  },
  "AccountContactRelation": {
    "AccountId": "0013z000035yYnMAAU"
  }
}
```

The `AccountContactRelation:AccountId` above is an `Id` of a Business Account record.

A Person Account record was created together with an Account Contact Relation record that associated the Person Account record with the Business Account record:

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/412805/Account-Contact-Relation-Record.png)

Hope this is useful...

Good luck!