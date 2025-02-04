# Use service\-linked roles for Amazon Connect<a name="connect-slr"></a>

Amazon Connect uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to Amazon Connect\. Service\-linked roles are predefined by Amazon Connect and include all the permissions that the service requires to call other AWS services on your behalf\.

A service\-linked role makes setting up Amazon Connect easier because you don't have to manually add the necessary permissions\. Amazon Connect defines the permissions of its service\-linked roles, and unless defined otherwise, only Amazon Connect can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

For information about other services that support service\-linked roles, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes** in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-linked role permissions for Amazon Connect<a name="slr-permissions"></a>

Amazon Connect uses the service\-linked role named **AmazonConnectServiceLinkedRolePolicy** – Grants Amazon Connect permission to access AWS resources on your behalf\.

The AmazonConnectServiceLinkedRolePolicy service\-linked role trusts the following services to assume the role:
+ `connect.amazonaws.com`

The role permissions policy allows Amazon Connect to complete the following actions on the specified resources\. As you enable additional features in Amazon Connect, additional permissions are added for the service\-linked role to access the resources associated with those features:
+ Action: all Amazon Connect actions, `connect:*`, on all Amazon Connect resources\.
+ Action: Amazon S3 `s3:GetObject`, `s3:GetObjectAcl`, `s3:PutObject`, `s3:PutObjectAcl`, `s3:DeleteObject`, `s3:GetBucketLocation`, and `GetBucketAcl` for the S3 bucket specified for recorded conversations\.

  It also grants `s3:PutObject`, `s3:PutObjectAcl`, and `s3:GetObjectAcl` to the bucket specified for exported reports\.
+ Action: Amazon Kinesis Data Firehose `firehose:DescribeDeliveryStream` and `firehose:PutRecord`, and `firehose:PutRecordBatch` for the delivery stream defined for agent event streams and CTRs\.
+ Action: Amazon Kinesis Data Streams `kinesis:PutRecord`, `kinesis:PutRecords`, and `kinesis:DescribeStream` for the stream specified for agent event streams and CTRs\.
+ Action: Amazon Lex `lex:PostContent` for the bots added to your instance\.
+ Action: Amazon Lex `lex:ListBots`, `lex:ListBotAliases` for the all bots created in the account across all Regions\.
+ Action: Amazon CloudWatch Logs `logs:CreateLogStream`, `logs:DescribeLogStreams`, and `logs:PutLogEvents` to the CloudWatch Logs group specified for contact flow logging\.
+ Action: High\-Volume Outbound Communications
  + `connect-campaigns:CreateCampaign`
  + `connect-campaigns:DeleteCampaign`
  +  `connect-campaigns:DescribeCampaign`
  + `connect-campaigns:UpdateCampaignName`
  + `connect-camapigns:GetCamapignState`
  +  `connect-camapigns:GetCamapignStateBatch`
  + `connect-camapigns:ListCampaigns`
  + `connect-campaigns:UpdateOutboundCallConfig`
  +  `connect-campaigns:UpdateDialerConfig`
  +  `connect-campaigns:PauseCampaign`
  + `connect-campaigns:ResumeCampaign`
  + `connect-campaigns:StopCampaign` for all operations related to high\-volume outbound campaigns\.

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-linked role permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

### Set up instances created before October 2018 to use service\-linked roles<a name="not-using-slr"></a>

If your instance was created before October 2018, you don't have service\-linked roles set up\. 

Add the **connect:\*** policy on the role that is associated with your Amazon Connect instance\. This enables you to access the public API for real\-time transcription, and real\-time transcription page that utilizes the API\.

## Create a srvice\-linked role for Amazon Connect<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When you create a new instance in Amazon Connect in the AWS Management Console, Amazon Connect creates the service\-linked role for you\.

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you create a new instance in Amazon Connect, Amazon Connect creates the service\-linked role for you again\. 

You can also use the IAM console to create a service\-linked role with the **Amazon Connect \- Full access** use case\. In the IAM CLI or the IAM API, create a service\-linked role with the `connect.amazonaws.com` service name\. For more information, see [Creating a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\. If you delete this service\-linked role, you can use this same process to create the role again\.

## Edit a service\-linked role for Amazon Connect<a name="edit-slr"></a>

Amazon Connect does not allow you to edit the AmazonConnectServiceLinkedRolePolicy service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Checking a service\-linked role has permissions for Amazon Lex<a name="check-slr"></a>

1. In the navigation pane of the IAM console, choose Roles\.

1. Choose the name of the role to modify\.

## Delete a service\-linked role for Amazon Connect<a name="delete-slr"></a>

You don't need to manually delete the AmazonConnectServiceLinkedRolePolicy role\. When you delete your Amazon Connect instance in the AWS Management Console,  Amazon Connect cleans up the resources and deletes the service\-linked role for you\.

## Supported Regions for Amazon Connect service\-linked roles<a name="slr-regions"></a>

Amazon Connect supports using service\-linked roles in all of the regions where the service is available\. For more information, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#connect_region)\.