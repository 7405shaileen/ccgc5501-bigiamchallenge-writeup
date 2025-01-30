# Challenge number
2

## Challenge Statement
Google Analytics
We created our own analytics system specifically for this challenge. We think it's so good that we even used it on this page. What could go wrong?

## IAM Policy 
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "sqs:SendMessage",
                "sqs:ReceiveMessage"
            ],
            "Resource": "arn:aws:sqs:us-east-1:092297851374:wiz-tbic-analytics-sqs-queue-ca7a1b2"
        }
    ]
}
```              
### write a short analysis about the IAM policy here
```
* What do I have access to?
Receive messages (sqs:ReceiveMessage)
Send messages (sqs:SendMessage)
* What don't I have access to?
Modify IAM policies related to the queue.
* What do I find interesting?
The IAM policy is too permissive. Attackers could read sensitive messages or inject malicious commands.
* etc
```

## Solution
Ranthe following command to see if you can access the SQS queue: aws sqs get-queue-attributes --queue-url https://<queue-url> --attribute-name All
The flag: {wiz:you-are-at-the-front-of-the-queue}

## Reflection
* What was your approach?
The exposed queue allowed me to receive messages
* What was the biggest challenge?
Finding the SQS queue URL
* How did you overcome the challenges?
Testing AWS commands step-by-step
* What led to the break through?
The ability to retrieve messages without authentication confirmed that the queue lacked proper access control.
* On the blue side, how can the learning be used to properly defend the important assets?
Ensure only trusted applications or roles have sqs:ReceiveMessage permissions.

