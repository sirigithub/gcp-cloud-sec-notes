## create new org:
The initial IAM policy for a newly created organization resource grants the Project Creator and Billing Account Creator roles to t
he entire Google Workspace domain. This means users will be able to continue creating project resources and billing accounts as they did before the 
organization resource existed. No other resources are created when an organization resource is created.

## project resources
In order to interact with most Google Cloud resources, you must provide the identifying project resource information for every request. You can identify a project resource in either of two ways: a project resource ID, or a project resource number (projectId and projectNumber in the code snippet).
