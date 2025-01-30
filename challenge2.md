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
* What don't I have access to?
* What do I find interesting?
* etc
```

## Solution
Detailed steps to the flag

## Reflection
* What was your approach?
* What was the biggest challenge?
* How did you overcome the challenges?
* What led to the break through?
* On the blue side, how can the learning be used to properly defend the important assets? 
