# Stack Exchange Question 418722

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/418856/dataraptor-how-to-do-a-for-each-comparison-formula)

## Answer

Unfortunately such transformation is not possible in a Dataraptor Extract, but luckily there are Dataraptor Transforms!

I managed to get the required result by wrapping everything in an Integration Procedure: 

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/418856/input-and-output.png)

I used:

1. Dataraptor Transform to extract all the matching list entries
2. Dataraptor Transform to extract all the non matching list entries
3. Merged the two lists
4. Returned the result in the required format

The Salesforce help files [here](https://help.salesforce.com/s/articleView?id=sf.os_function_reference_56716.htm&type=5) lists the function `FILTER` with some examples on how to extract a list entry with certain criteria. I ended up using:

`FILTER(LIST(FORMULA_List), 'FirstName == "' + FIRST_NAME + '"')`

which returns a list of all the list entries where the `FirstName` matches the string assigned to `FIRST_NAME`. `FORMULA_List` contained the `NameHistory` list.

I used the same formula to extract all the list entries that does not match, but changed it so that `'FirstName <> "' + FIRST_NAME + '"'`

In the Dataraptor Transform you can also add the additional JSON property `isFirstNameMatchWithChild` with its corresponding value and then return the transformed list to the Integration Procedure. 

While it is not all contained in one Dataraptor as your question asked, I do feel it is better to break all the actions up in different parts which ultimately helps with debugging.

Good luck!