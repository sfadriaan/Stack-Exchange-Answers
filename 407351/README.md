# Stack Exchange Question 407351

## Question

Question can be found [here](https://salesforce.stackexchange.com/questions/407351/close-embedded-custom-lwc-flyout-modal/419601#419601)

## Answer

I had a scenario where I wanted to automatically close an Omniscript that was displayed as a flyout. 

The Salesforce documentation [here](https://help.salesforce.com/s/articleView?id=sf.os_fire_an_event_to_automatically_close_a_flyout_modal.htm&type=5) is quite useful in how to go about doing it.

High level steps of my setup are:

1. Click Action that opens flyout.
2. Run through Omniscript and at the end trigger a data pubsub via a Set Value element.
3. Flexcard listens for this data pubsub and closes the flyout when it is received.

Basically, when you create an action on the Flexcard that launches the flyout, you will see there is a Channel Name specified as `close_modal`:

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/407351/close-modal-channel-name.png)

Under the Setup tab of the Flexcard, you then add an Event Listener that listens for the event that triggers to close the flyout (in my case it was the data pubsub):

![](https://github.com/sfadriaan/Stack-Exchange-Answers/blob/main/407351/flexcard-event-listener.png)

you then reference the relevant pubsub event and create an Event Action that points to the Channel Name `close_modal` with the Event Name as `close`.

For your use case, the custom LWC will have to publish an event that the flexcard can subscribe to and then close the flyout when the Flexcard receives the pubsub.

Good luck!