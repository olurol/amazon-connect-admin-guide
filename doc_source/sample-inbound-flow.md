# Sample inbound flow \(first contact experience\)<a name="sample-inbound-flow"></a>

Type: Contact flow \(inbound\)

This sample flow is automatically assigned to the phone number that you claimed when you first set up contact flows\. For more information, see [Get started](amazon-connect-get-started.md)\. 

It uses **Check contact attributes** to determine if the contact is contacting you by phone or chat, or if it is a task, and to route them accordingly\.
+ If the channel is chat or task, the contact is transferred to the **Set disconnect flow**\.
+ If the channel is voice, then based on user input the contact is either transferred to the other sample contact flows or a sample follow\-up agent task is created for this contact\. 