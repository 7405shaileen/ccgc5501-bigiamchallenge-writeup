# Cloudfoxable 4 Lab Report

## Overview

The lab exercise involved extracting a hidden "flag" from AWS Systems Manager (SSM) using IAM roles and permissions. The main tasks included:

- **Assuming a specified IAM role:** Described as "Ertz" in a starter account.
- **Troubleshooting role assumption failures:** Identifying and resolving issues when role assumption did not work.
- **Extracting a secret safely:** Using the AWS CLI.

## Initial Configuration

I initiated the exercise as a `non-root-user` with Admin privileges. I then discovered that my account was not permitted to assume the `Ertz` role because the role's trust policy was configured to grant access only to the `ctf-starting-user`.

## Step-by-Step Process

### 1. First Attempt: Role Assumption Failure

I began by executing the following command:

```bash
aws --profile cloudfoxable sts assume-role --role-arn arn:aws:iam::307946660251:role/Ertz --role-session-name Ertz
````
This attempt failed because my active user wasn't recognized by the role's trust policy. Upon reviewing the policy, I found that my non-root-user was not defined as an authorized principal.
### 2. Upgrading the Trust Policy
The solution was to update the trust policy for the Ertz role so that it included both my account and the initially authorized user. The modified policy was:

````
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": {
      "AWS": [
        "arn:aws:iam::307946660251:user/ctf-starting-user",
        "arn:aws:iam::307946660251:user/non-root-user"
      ]
    },
    "Action": "sts:AssumeRole"
  }]
}
````
### 3. Successful Role Assumption
After updating the trust policy, I executed the assume-role command again. This time, it was successful, and I received temporary credentials to operate under the Ertz role.

### 4. Retrieving the Secret
With the necessary permissions, I proceeded to extract the secret flag using the AWS CLI command:

aws ssm get-parameter --name "/cloudfoxable/flag/its-another-secret" --with-decryption --region us-west-2

The output returned the flag:
FLAG{ItsAnotherSecret::ThereWillBeALotOfAssumingRolesInThisCTF}

### 5. Checking Permissions
I verified that the Ertz role had an appropriate policy attached that granted access to SSM. This confirmed that the secret could be successfully retrieved once the role was assumed.

## Reflections and Key Takeaways
- **Primary Challenge:** Ensuring the JSON format of the trust policy was correct.
- **Key Insight:** Explicitly including my user ARN in the role's trust relationship was critical.

## Key Insight: 
Explicitly including my user ARN in the role's trust relationship was critical.

## Security Best Practices
- **Least Privilege:** Follow the principle of least privilege to avoid excessive permissions.
- **Regular Audits:** Regularly audit and review trust policies.
- **Secure Storage:** Always store sensitive data in secure systems like SSM or Secrets Manager instead of plaintext.
