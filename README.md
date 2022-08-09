# gcp-cloud-sec-notes

### Super admin
* what is a super admin? Well,
it's the user that you use to sign up for Google Cloud,
and this user has super admin access to the entire organization.
* It is by far the most powerful user in your system.
But what makes it even more powerful is that these permissions cannot
be revoked.
* It should be used with caution and should only be used in an emergency or
high-level functions, such as admin account recovery

### G Suite Domain
* virtual group of all the accounts that have been created
* A special identifier that represents every authenticated gcp account
* policies are represented by an iam policy object
* IAM policy is represented by an object which is combination of binding and role
* binding = member + role

### Access scopes vs IAM roles
* A more restrictive access scope will over ride a permissive IAM role
* Default service account for compute will come up with scopes, custom sa for compute will come up with IAM roles. 
