# About contact attributes in a rule<a name="rules-task-contact-attributes"></a>

You can have up to 5 contact attributes in a rule\.

You can design contact flows to use the contact attributes you specify in a rule, and then route the task accordingly\. For example, a call arrives in your contact center\. When Contact Lens analyzes the call, it gets a hit on the **Compliance** rule\. The CTR that's created for the call includes information similar to the following image: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-attributes-example1.png)

The Rules engine generates a task\. The CTR for the task inherits contact attributes from the voice CTR, as illustrated in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-attributes-example2.png)

The voice CTR appears as the **Previous contact ID**\. 

The contact flow that you specify in the rule should be designed to use the contact attributes and route the task to the appropriate owner\. For example, you may want to route tasks where **CustomerType = VIP** to a specific agent\.

For more information, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\.