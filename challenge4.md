# Challenge number
4

## Challenge Statement
Admin only?
We learned from our mistakes from the past. Now our bucket only allows access to one specific admin user. Or does it?
## IAM Policy 
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                },
                "ForAllValues:StringLike": {
                    "aws:PrincipalArn": "arn:aws:iam::133713371337:user/admin"
                }
            }
        }
    ]
}
```              
### write a short analysis about the IAM policy here
```
* What do I have access to?
s3:GetObject: Allows any principal ("Principal": "*") to retrieve objects from the bucket thebigiamchallenge-admin-storage-abf1321.
s3:ListBucket: Permits any principal to list objects in the bucket

* What don't I have access to?
Listing Objects Without Matching Conditions: If the principal's ARN doesn't match arn:aws:iam::133713371337:user/admin, they cannot list objects in the bucket, even if the object key starts with files/.
Listing Objects Outside the 'files/' Prefix: 

* What do I find interesting?
The policy allows any principal to retrieve any object from the bucket without restrictions, which poses a security risk.
The s3:ListBucket action is restricted by both the object key prefix and the principal's ARN, indicating an attempt to limit access to specific users and objects.

* etc
```

## Solution
Attempt to list objects in the bucket using the AWS CLI: aws s3 ls s3://thebigiamchallenge-admin-storage-abf1321/files/
Retrieve the Flag:     aws s3 cp s3://thebigiamchallenge-admin-storage-abf1321/files/flag-as-admin.txt .
                       cat flag-as-admin.txt

## Reflection
* What was your approach?
I analyzed the IAM policy to understand the permissions granted and the conditions applied. Then, I attempted to list and access objects in the S3 bucket based on the policy's allowances.

* What was the biggest challenge?
Understanding the implications of the ForAllValues:StringLike condition and how it interacts with the aws:PrincipalArn condition key.

* How did you overcome the challenges?
By testing the permissions using the AWS CLI, I observed that the s3:ListBucket action was permitted despite the conditions, indicating a misconfiguration or misunderstanding of the policy's intent.

* What led to the break through?
Realizing that the s3:GetObject permission was overly permissive allowed me to access the flag without needing to satisfy the s3:ListBucket conditions.

* On the blue side, how can the learning be used to properly defend the important assets?
Limit s3:GetObject permissions to specific principals rather than allowing all principals.
Regularly review IAM policies and test them to ensure they enforce the intended access controls.
