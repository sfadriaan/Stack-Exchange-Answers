# Stack Exchange Question 411024

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/411024/is-this-transformation-even-possible-using-an-dataraptor/417540#417540)

## Answer

There are Salesforce documentation [here](https://help.salesforce.com/s/articleView?id=sf.os_manipulate_json_with_the_send_response_transformations_properties_22367.htm&type=5) which shows how to reparent the node dynamically using merge field syntax. 

Using the logic in the mentioned documentation, you can create an Integration Procedure which transforms each list entry to its desired form. 
High level steps include:

1. Get value of `Name` node for the relevant list
2. Transform List entry to only have the required key:value pairs
3. Assign the retrieved value of the `Name` node as the new node name for the transformed list entry

This will basically transform a list entry:
```
{
    "Name": "a",
    "Type": "t1",
    "Size": "s"
}
```
to the required format of:
```
{
  "a": {
    "Size": "s",
    "Type": "t1"
  }
}
```
I found it easiest to use the Integration Procedure in another Integration Procedure.
This was purely to make debugging easier, as I prefer little chunks rather than one big thing.

The parent Integration Procedure has a loop element that loops over all the list entries and builds the new list as it goes. 
I ended up with the required format but it went from `c` to `a` which I assume is not a problem as you can easily get the values you want by using merge field syntax such as `Data:a` or `Data:c`.

You can download the Datapack [here](https://github.com/sfadriaan/Stack-Exchange-Answers/tree/main/411024) to play around with.

Good luck!