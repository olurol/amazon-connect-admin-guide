# Monitoring your instance using CloudWatch<a name="monitoring-cloudwatch"></a>

Amazon Connect sends data about your instance to CloudWatch metrics so that you can collect, view, and analyze CloudWatch metrics for your Amazon Connect virtual contact center\. You can use this data to monitor key operational metrics and set up alarms\. Data about your contact center is sent to CloudWatch every 1 minute\.

When you view the CloudWatch metrics dashboard, you can specify the refresh interval for the data displayed\. The values displayed in the dashboard reflect the values for the refresh interval you define\. For example, if you set the refresh interval to 1 minute, the values displayed are for a minute period\. You can select a refresh interval of 10 seconds, but Amazon Connect does not send data more often than every 1 minute\. Metrics that are sent to CloudWatch are available for two weeks, and then discarded\. To learn more about metrics in CloudWatch, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\.

## Amazon Connect metrics sent to CloudWatch<a name="connect-metrics-cloudwatch"></a>

The `AWS/Connect` namespace includes the following metrics\.

**CallsBreachingConcurrencyQuota**  
The total number of voice calls that exceeded the concurrent calls quota for the instance\. For the total number of calls that breach the quota, take a look at the Sum statistic\.  
For example, assume your contact center experiences the following volumes, and your service quota is 100 concurrent calls:  
+ 0:00 : 125 concurrent calls\. This is 25 over the quota\. 
+ 0:04 : 135 concurrent calls\. This is 35 over the quota\. 
+ 0:10 : 150 concurrent calls\. This is 50 over the quota\. 
CallsBreachingConcurrencyQuota = 110: the total number of voice calls that exceeded the quota between 0:00 and 0:10\.  
Unit: Count  
Dimension:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**CallBackNotDialableNumber**  
The number of times a queued callback to a customer could not be dialed because the customer's number is in a country for which outbound calls are not allowed for the instance\. The countries allowed for an instance are defined by the service quotas\.  
Unit: Count  
Dimensions:  
+ **InstanceId** The ID of your instance
+ **MetricGroup**: **ContactFlow**
+ **ContactFlowName**: The name of your contact flow

**CallRecordingUploadError**  
The number of call recordings that failed to upload to the Amazon S3 bucket configured for your instance\. This is the bucket specified in **Data Storage** > **Call Recordings** settings for the instance\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **CallRecordings**

**CallsPerInterval**  
The number of voice calls, both inbound and outbound, received or placed per second in the instance\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ConcurrentCalls**  
The number of concurrent active voice calls in the instance at the time the data is displayed in the dashboard\. The value displayed for this metric is the number of concurrent active calls at the time the dashboard is displayed, and not a sum for the entire interval of the refresh interval set\. All active voice calls are included, not only active calls that are connected to agents\.  
While all statistics are available in CloudWatch for concurrent voice calls you might be most interested in looking at the Maximum/Average statistic\. The Sum statistic isn't as useful here\.   
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ConcurrentCallsPercentage**  
The percentage of the concurrent active voice calls service quota used in the instance\. This is calculated by:  
+ ConcurrentCalls / ConfiguredConcurrentCallsLimit
Unit: Percent \(output displays as a decimal\)  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ConcurrentTasks**  
The number of concurrent active tasks in the instance at the time the data is displayed in the dashboard\. The value displayed for this metric is the number of concurrent active tasks at the time the dashboard is displayed, and not a sum for the entire interval of the refresh interval set\. All active tasks are included, not only active tasks that are connected to agents\.  
While all statistics are available in CloudWatch for concurrent tasks you might be most interested in looking at the Maximum/Average statistic\. The Sum statistic isn't as useful here\.   
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Tasks**

**ConcurrentTasksPercentage**  
The percentage of the concurrent active tasks service quota used in the instance\. This is calculated by:   
+ ConcurrentTasks / ConfiguredConcurrentTasksLimit 
Where ConfiguredConcurrentTasksLimit is the [Concurrent tasks per instance](amazon-connect-service-limits.md) configured for your instance\.   
Unit: Percent \(output displays as a decimal\)  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Tasks**

**ContactFlowErrors**  
The number of times the error branch for a contact flow was run\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **ContactFlow**
+ **ContactFlowName**: The name of your contact flow

**ContactFlowFatalErrors**  
The number of times a contact flow failed to execute due to a system error\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **ContactFlow**
+ **ContactFlowName**: The name of your contact flow

**LongestQueueWaitTime**  
The longest amount of time, in seconds, that a contact waited in a queue\. This is the length of time a contact waited in a queue during the refresh interval selected in the CloudWatch dashboard, such as 1 minute or 5 minutes\.  
Unit: Seconds  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Queue**
+ **QueueName**: The name of your queue

**MissedCalls**  
The number of voice calls that were missed by agents during the refresh interval selected, such as 1 minute or 5 minutes\. A missed call is one that is not answered by an agent within 20 seconds\.  
To monitor the total missed calls in a given time period, take a look at the Sum statistic in CloudWatch\.  
Unit: Seconds  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**MisconfiguredPhoneNumbers**  
The number of calls that failed because the phone number is not associated with a contact flow\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**PublicSigningKeyUsage**  
The number of times a contact flow security key \(public signing key\) was used to encrypt customer input in a contact flow\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **SigningKeyId**: The ID of your signing key

**QueueCapacityExceededError**  
The number of calls that were rejected because the queue was full\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Queue**
+ **QueueName**: The name of your queue

**QueueSize**  
The number of contacts in the queue\. The value reflects the number of contacts in the queue at the time the dashboard is accessed, not for the duration of the reporting interval\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Queue**
+ **QueueName**: The name of your queue

**TasksBreachingConcurrencyQuota**  
The total number of tasks that exceeded the concurrent tasks quota for the instance\. For the total number of tasks that breach the quota, take a look at the Sum statistic\.   
For example, assume your contact center experiences the following volumes, and your service quota is 2500 concurrent tasks:   
+ 0:00 : 2525 concurrent tasks\. This is 25 over the quota\.
+ 0:04 : 2535 concurrent tasks\. This is 35 over the quota\.
+ 0:10 : 2550 concurrent tasks\. This is 50 over the quota\.
 TasksBreachingConcurrencyQuota = 110: the total number of tasks that exceeded the quota between 0:00 and 0:10\.   
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Tasks**

**TasksExpired**  
 Tasks which have expired after being active for 7 days\.   
To monitor the total number of tasks that have expired in a given time period, take a look at the Sum statistic in CloudWatch\.   
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Tasks**
+ **ContactId**: The ID of the task contact

**TasksExpiryWarningReached**  
Tasks that have been active for 6 days 22 hours and reached expiry warning limit\.   
To monitor the total number of tasks that have reached expiry warning limit in a given time period, take a look at the Sum statistic in CloudWatch\.   
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Tasks**
+ **ContactId**: The ID of the task contact

**ThrottledCalls**  
The number of voice calls that were rejected because the rate of calls per second exceeded the maximum supported quota\. To increase the supported rate of calls, request an increase in the service quota for concurrent active calls per instance\.  
To monitor the total throttled calls in a given time period, take a look at the Sum statistic in CloudWatch\.  
Unit: Seconds  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ToInstancePacketLossRate**  
The ratio of packet loss for calls in the instance, reported every 10 seconds\. Each data point is between 0 and 1, which represents the ratio of packets lost for the instance\.  
Unit: Percent  
Dimensions:  
+ **Participant**: **Agent**
+ **Type of Connection**: **WebRTC**
+ **Instance ID**: The ID of your instance
+ **Stream Type**: **Voice**

## Amazon Connect CloudWatch metrics dimensions<a name="connect-cloudwatch-dimensions"></a>

In CloudWatch, a dimension is a name/value pair that uniquely identifies a metric\. In the dashboard, metrics are grouped by dimension\. When you view metrics in the dashboard, only metrics with data are displayed\. If there is no activity during the refresh interval for which there is a metric, then no data from your instance is displayed in the dashboard\.

The following dimensions are used in the CloudWatch dashboard for Amazon Connect metrics\. 

### Contact flow metrics dimension<a name="contact-flow-dimension"></a>

**Note**  
If a contact flow has a dimension name in non\-ASCII characters, you won't be able to see it in CloudWatch\. 

Filters metric data by contact flow\. Includes the following metrics:
+ ContactFlowErrors
+ ContactFlowFatalErrors
+ PublicSigningKeyUsage

### Contact metrics dimension<a name="contact-metrics-dimension"></a>

Filters metric data by contacts\. Includes the following metrics:
+ TasksExpiryWarningReached
+ TasksExpired

### Instance metrics dimension<a name="instance-metrics-dimension"></a>

Filters meta data by instance\. Includes the following metrics:
+ CallsBreachingConcurrencyQuota
+ CallsPerInterval
+ CallRecordingUploadError
+ ConcurrentCalls
+ ConcurrentCallsPercentage
+ ConcurrentTasks
+ ConcurrentTasksPercentage
+ MisconfiguredPhoneNumbers
+ MissedCalls
+ TasksBreachingConcurrencyQuota
+ ThrottledCalls

### Instance ID, Participant, Stream Type, Type of Connection<a name="stream-type-dimension"></a>

Filters metric data by connection\. Includes the following metrics:
+ ToInstancePacketLossRate

### Queue metrics dimension<a name="queue-metrics-dimension"></a>

**Note**  
If a queue has a dimension name in non\-ASCII characters, you won't be able to see it in CloudWatch\. 

Filters metric data by queue\. Includes the following metrics:
+ CallBackNotDialableNumber
+ LongestQueueWaitTime
+ QueueCapacityExceededError
+ QueueSize

## Amazon Connect Voice ID metrics sent to CloudWatch<a name="voiceid-metrics-cloudwatch"></a>

The `VoiceID` namespace includes the following metrics\.

**RequestLatency**  
The elapsed time for the request\.  
Frequency: 1 minute  
Unit: Milliseconds  
Dimension: API

**UserErrors**  
The number of Error counts due to bad requests from user\.  
Frequency: 1 minute  
Unit: Count  
Dimension: API

**SystemErrors**  
The number of Error counts due to internal service error\.  
Frequency: 1 minute  
Unit: Count  
Dimension: API

**Throttles**  
The number of requests that are rejected due to exceeding the max rate allowed for sending requests\.  
Frequency: 1 minute  
Unit: Count  
Dimension: API

**ActiveSessions**  
The number of active sessions in the domain\. Active sessions are sessions that are in pending or ongoing status\.  
Frequency: 1 minute  
Unit: Count  
Dimension: Domain

**ActiveSpeakerEnrollmentJobs**  
The number of active Batch Enrollment Jobs in the domain\. Active Jobs are those which are in Pending or InProgress status\.  
Frequency: 15 minutes  
Unit: Count  
Dimension: Domain

**ActiveFraudsterRegistrationJobs**  
The number of active Batch Registration Jobs in the domain\. Active Jobs are those which are in Pending or InProgress status\.   
Frequency: 15 minutes  
Unit: Count  
Dimension: Domain

**Speakers**  
The number of Speakers in the domain\.  
Frequency: 15 minutes  
Unit: Count  
Dimension: Domain

**Fraudsters**  
The number of Fraudsters in the domain\.  
Frequency: 15 minutes  
Unit: Count  
Dimension: Domain

## Amazon Connect Voice ID metrics dimensions<a name="voiceid-cloudwatch-dimensions"></a>

The following dimensions are used in the CloudWatch dashboard for Amazon Connect Voice ID metrics\. When you view metrics in the dashboard, only metrics with data are displayed\. If there is no activity during the refresh interval for which there is a metric, then no data from your instance is displayed in the dashboard\.

### API metrics dimension<a name="voiceid-api-dimension"></a>

This dimension limits the data to one of the following Voice ID operations:
+ DeleteFraudster
+ EvaluateSession
+ ListSpeakers
+ DeleteSpeaker
+ OptOutSpeaker

### Domain metrics dimension<a name="voiceid-domain-dimension"></a>

The Voice ID domain where the enrollment, authentication or registration is conducted\. 

## Use CloudWatch metrics to calculate concurrent call quota<a name="connect-cloudwatch-concurrent-call-quota"></a>

Here's how to calculate your quota for concurrent calls\. 

With calls active in the system, look at **ConcurrentCalls** and **ConcurrentCallsPercentage**\. Calculate the quota: 
+ \(ConcurrentCalls / ConcurrentCallsPercentage\) \* 100

For example, if **ConcurrentCalls** is 20 and **ConcurrentCallsPercentage** is 50, your quota is calculated as \(20/50\)\*100 = 40\.

## Use CloudWatch metrics to calculate concurrent task quota<a name="connect-cloudwatch-concurrent-task-quota"></a>

Here's how to calculate your quota for concurrent tasks\. 

With tasks active in the system, look at **ConcurrentTasks** and **ConcurrentTasksPercentage**\. Calculate the quota: 
+ \(ConcurrentTasks / ConcurrentTasksPercentage\) \* 100

For example, if **ConcurrentTasks** is 20 and **ConcurrentTasksPercentage** is 50, your quota is calculated as \(20/50\)\*100 = 40\.