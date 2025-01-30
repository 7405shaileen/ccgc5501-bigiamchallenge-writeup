# Challenge number
1

## Challenge Statement
Buckets of Fun
We all know that public buckets are risky. But can you find the flag?

## IAM Policy 
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                }
            }
        }
    ]
}
```              
### write a short analysis about the IAM policy here

* What do I have access to?
The S3 bucket allows me to list (s3:ListBucket) and retrieve (s3:GetObject) objects within the files/ prefix.
* What don't I have access to?
I do not have permission to modify (s3:PutObject or s3:DeleteObject) or upload new files.
I cannot access objects outside the files/ prefix.
* What do I find interesting?
The IAM policy grants public read access to certain objects, which poses a significant security risk.
* etc


## Solution
Detailed steps to the flag
First, check what permissions I have using AWS CLI which lists all the objects inside the files/ directory
From the output, I find flag1.txt, which is likely the target file.
Using the s3 cp command, I download the flag
Opening the file reveals the flag: {wiz:exposed-storage-risky-as-usual}

## Reflection
* What was your approach?
My approach was to analyze the S3 bucket’s IAM policy to determine the level of access granted. Once I identified the flag1.txt file, I downloaded it using aws s3 cp s3://<bucket-name>/files/flag1.txt . to retrieve the flag.
* What was the biggest challenge?
The biggest challenge was ensuring that I had the correct permissions to access the bucket and understanding the impact of overly permissive IAM policies.
* How did you overcome the challenges?
I overcame these challenges by methodically testing the available permissions. Using enumeration techniques, I verified which objects were accessible.
* What led to the break through?
The breakthrough came from recognizing that the IAM policy permitted public access to the files/ prefix. 
* On the blue side, how can the learning be used to properly defend the important assets?
Restrict S3 bucket access only to authorized users.
Regularly review and refine IAM policies
