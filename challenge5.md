Reflection on AWS Account Setup

Introduction
Setting up a secure AWS environment requires careful planning. This reflection covers creating a new AWS account, setting up a non-root user, generating access keys, configuring AWS CLI, enabling MFA, and granting administrative access.

Account Setup and User Configuration
After creating a new AWS account, I set up a non-root IAM user to reduce security risks associated with using root credentials. Using the IAM Dashboard, I navigated to Users under Access Management, created a new user, and assigned appropriate permissions.

Granting Administrative Access
To enable administrative tasks for the non-root user, I attached the AdministratorAccess policy:
1.	Opened IAM Dashboard.
2.	Selected Users and chose the non-root user.
3.	Attached the AdministratorAccess policy under Permissions.

This allowed full administrative control without relying on the root account.
Access Keys and AWS CLI Configuration

For programmatic access, I generated access keys for both root and non-root users. I then configured AWS CLI:
aws configure

Enabling Multi-Factor Authentication (MFA)
To enhance security, I enabled MFA for both accounts:
1.	Opened IAM Dashboard.
2.	Selected the user accounts.
3.	Clicked Manage MFA and linked an authentication device.

Key Security Takeaways
•	Use Root Account Sparingly: Only for critical management tasks.
•	Role-Based Access Control (RBAC): Assign only necessary privileges.
•	MFA is Essential: Adds an extra layer of protection.
•	Secure Key Management: Prevents credential leaks.
•	Least Privilege Principle: Regularly review and minimize access rights.

Conclusion
This process reinforced the importance of AWS security best practices. Properly configuring accounts ensured effective access control while reducing attack surfaces. Maintaining these best practices will be critical for long-term cloud security management.
