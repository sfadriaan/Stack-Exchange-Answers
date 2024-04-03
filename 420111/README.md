# Stack Exchange Question 420111

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/420111/sum-up-items-in-a-flex-card/420237#420237)

## Answer

For data extraction and transformation requirements other than just retrieving data, I would opt to wrap everything in an Integration Procedure and tailor the response to properly display the information in the flexcard.

The JSON that the Flexcard needs to receive should be something like:

```json
{
  "QuoteLineItem": [
    {
      "ProductName": "QuoteLine 1",
      "TotalPrice": 7
    },
    {
      "ProductName": "QuoteLine 2",
      "TotalPrice": 5
    },
    {
      "ProductName": "QuoteLine 3",
      "TotalPrice": 15
    },
    {
      "ProductName": "QuoteLine 4",
      "TotalPrice": 1000
    }
  ],
  "GrandTotal": 1027
}
```

In order to sum the `TotalPrice` field, you can use the sum function. See Salesforce help files [here](https://help.salesforce.com/s/articleView?id=sf.os_function_reference_56716.htm&type=5)

The formula would look something like this:

```
SUM(QuoteLiteItem:TotalPrice)
```

I put the formula in a Set Value Action and then used the Response Action to create the response JSON:

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/420111/integration-procedure.png)

You can then use a merge field on the parent Flexcard for displaying the `Grand Total` and the child Flexcard to display the Quote Line Items:

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/420111/flexcard.png)

Good luck!