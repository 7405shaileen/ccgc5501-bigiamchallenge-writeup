CloudFoxable Challenge 1 - Do This First

Overview
The first CloudFoxable challenge, "Do This First," introduces fundamental cloud security enumeration techniques. The goal is to authenticate using AWS credentials, identify accessible resources, and retrieve the first flag.

Methodology
Step 1: AWS CLI Configuration
The challenge provided AWS credentials, which I configured with:
aws configure
After entering the Access Key and Secret Key, authentication was successful.
To confirm that my CLI was working, I executed the following command:
aws sts get-caller-identity

Step 2: IAM User Enumeration
To identify the IAM user associated with my credentials, I ran:
aws iam list-users
This confirmed that I had access to an IAM user.

Step 3: Checking Permissions
To determine what permissions were granted, I listed attached policies:
aws iam list-attached-user-policies --user-name non-rootuser
The results indicated read access to S3.

Step 4: Enumerating S3 Buckets
With S3 read access confirmed, I listed the available S3 buckets:
aws s3 ls
A bucket named cloudfoxable-flag-bucket was present. Listing its contents:
aws s3 ls s3://cloudfoxable-flag-bucket
revealed a file named flag.txt.

Step 5: Retrieving the Flag
To access the flag, I executed:
aws s3 cp s3://cloudfoxable-flag-bucket/flag.tx


The flag obtained was:
FLAG{congrats_you_are_now_a_terraform_expert_happy_hunting}

Conclusion
This challenge reinforced essential AWS enumeration techniques, such as IAM policy inspection and S3 bucket access.
