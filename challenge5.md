Reflection on AWS Account Security Setup

Introduction
Setting up a secure AWS environment requires careful planning. This reflection covers creating a new AWS account, setting up a non-root user, generating access keys, configuring AWS CLI, enabling MFA, and granting administrative access.

Account Setup and User Configuration
After creating a new AWS account, I set up a non-root IAM user to reduce security risks associated with using root credentials. Using the IAM Dashboard, I navigated to Users under Access Management, created a new user, and assigned appropriate permissions.

Granting Administrative Access
To enable administrative tasks for the non-root user, I attached the AdministratorAccess policy:

Opened IAM Dashboard.
Selected Users and chose the non-root user.
Attached the AdministratorAccess policy under Permissions.
This allowed full administrative control without relying on the root account.

Why Create an Admin User When Root Exists?
While the root account has full privileges, it should only be used for essential management functions, such as account recovery and billing. An admin IAM user enables better security control, auditability, and least privilege enforcement while reducing the risk of compromising critical account-wide settings.

Access Keys and AWS CLI Configuration
For programmatic access, I generated access keys for both root and non-root users. Root keys were removed after testing, while non-root keys were securely stored. I then configured AWS CLI:

aws configure

Enabling Multi-Factor Authentication (MFA)
To enhance security, I enabled MFA for both accounts:

Opened IAM Dashboard.
Selected the user accounts.
Clicked Manage MFA and linked an authentication device.
MFA significantly reduced the risk of unauthorized access.

Security Measures Implemented and Their Importance
Non-root IAM user – Prevents over-reliance on the root account, reducing security risks.
AdministratorAccess for IAM user – Ensures operational flexibility while restricting root usage.
Access Key Generation for CLI – Enables secure automation without exposing sensitive credentials.
MFA Activation – Adds an extra authentication layer to protect against credential leaks.
Secure Key Management – Ensures keys are not stored in plaintext or shared carelessly.
Least Privilege Principle – Ensures only necessary access is granted, limiting attack surfaces.

Key Security Takeaways
Use Root Account Sparingly: Only for critical management tasks.
Role-Based Access Control (RBAC): Assign only necessary privileges.
MFA is Essential: Adds an extra layer of protection.
Secure Key Management: Prevents credential leaks.
Least Privilege Principle: Regularly review and minimize access rights.

Conclusion
This process reinforced the importance of AWS security best practices. Properly configuring accounts ensured effective access control while reducing attack surfaces. Maintaining these best practices will be critical for long-term cloud security management.

