# Stack Exchange Question 416744

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/416744/pass-recordid-as-input-for-custom-lwc-embeeded-in-a-flexcard/417326#417326)

## Answer

I am assuming the `{recordId}` you want to pass to the custom LWC is the `accountId`?
By default, the `recordId` is always available as a property on App pages and record pages. See Salesforce documentation [here][1]. You can confirm this by going to your activated Flexcard's Publish Options and on the Editor tab, you will see it listed:

![](https://github.com/sfadriaan/stack-exchange-answers/blob/main/416744/How-To-Get-To-Publish-Options.png)

![](https://github.com/sfadriaan/stack-exchange-answers/blob/main/416744/Publish-Options-Editor.png)

As you are already using the merge field `{recordId}` to pass the recordId to the custom LWC, it might be good to add some debugging text just to see that the `recordId` is in fact included in the `{recordId}` merge field. 

You can do this by adding a Rich Text field to your Flexcard and adding something in the line of `RecordId: {recordId}` in its Text Properties. 

Activate your flexcard, embed it where it needs to be embedded (assuming again it is the Account record page) and see if the merge field updates with the corresponding `recordId` for different Account records. I built a minimal working example Flexcard that shows the `recordId` of the record where it is embedded:

![](https://github.com/sfadriaan/stack-exchange-answers/blob/main/416744/AccountId1.png)

![](https://github.com/sfadriaan/stack-exchange-answers/blob/main/416744/AccountId2.png)

![](https://github.com/sfadriaan/stack-exchange-answers/blob/main/416744/AccountId3.png)

Once you have determined that the `recordId` is passed correctly to the merge field, then you can try and pass it to the custom LWC.

If it still doesn't work, then at least you know the issue is not with the merge field, but rather somewhere else.

Good luck!