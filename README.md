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

### Encryption
* All data at rest is encrypted at rest.
* Types of encryption
 * Encryption by default
 * Cloud key management service
 * Customer supplied encryption keys
* When data is uploaded to storage it is broken into chunks and each chunk is encrypted using using a different key, if data is updated it is encrypted using a new key , so the old key is never updated.
* Now, each of these chunks is encrypted at the storage level with its own
unique encryption key. So,
each chunk has its own key and no two chunks will have the
same encryption key,
even if they are part of the same Google Cloud storage object,
if they're owned by the same customer,
or if they are stored on the same machine.
These encryption keys are unique.
And so each updated chunk is encrypted with a new key
every time it's updated. So, the old key is never updated --
merely replaced with a new key. And once each chunk is encrypted,
the chunks are then distributed across Google's storage infrastructure with its
corresponding encryption key

* Cloud KMS is a central repository for storing KEKs.
Here you are able to generate, use,
rotate, and destroy symmetric encryption keys,
as we were discussing earlier on in encryption overview.
Now, KEKs are not exportable from KMS,
and this is by design due to encryption and decryption being done
with keys only in KMS.

* data is chunked and encrypted with DEKs.
DEKs are then encrypted with KEKs.
KEKs are stored within KMS.
And then KMS keys are wrapped with the KMS master key,
which is stored in Root KMS.
Root KMS keys are then wrapped with the root KMS master key,
which is stored in the root KMS master key distributor

* CSEKs are only available for compute engine and storage only.
* 

#### Cloud DLP
Used to scan data for PII or sensitive data types
select from built in data patterns for global or country specific types of sensitive data

#### BigQuery :
dataset , table or view level access control
sub table access control

#### cloud storage:
bucket level or object level access control
cloud iam or acl

Tools used in combination for secure ci/cd deployments:
* checked in code
* cloud build
* CSR vulnerability scanning 
* Binary auth

### Shielded VMs

Shielded VMs are virtual machines (VMs) on Google Cloud hardened by a set of security controls that help defend against rootkits and bootkits. Using Shielded VMs helps protect enterprise workloads from threats like remote attacks, privilege escalation, and malicious insiders.

Set an organization-level policy that requires all Compute Engine VMs to be configured as
Shielded VMs. Use Measured Boot enabled with Virtual Trusted Platform Module (vTPM). Validate
integrity events in Cloud Monitoring and place alerts on late boot validation events.

Shielded VMs offer Virtual Trusted Platform Module (vTPM) which enables integrity
monitoring. A vTPM generates hashes for the boot event and sandwiches all
subsequent actions as updates to the hash. The final hash is used to validate against
the hashes of every reboot. Any changes, updates, or misconfigurations at boot time
can be captured at this stage.

Compute Engine images provide reusability and ease of redeployment. Images can
be built from a persistent disk or its snapshot or from an existing image. This existing
image could be in a project or Cloud Storage. Shielded VMs leverage the image
reusability only if firmware is UEFI-compliant, and you can enable secure boot in
images.
Shell scripts and Cloud Build can be used to automate the image creation process if
the task is small and does not require a complete CI/CD pipeline. Before creating the
image, ensure that the instance is stopped.

### Cloud Audit logs
* provide complete cover of administrative activity
* capture reads and writes to managed data store
* export logs for long term storage

When you create a GKE cluster, Cloud Logging is enabled by default. Both Google
Cloud and the Kubernetes ecosystem provide a range of tools for forensic
investigations and audit. Cloud Logging, Docker-explorer, and Kubectl Sysdig Capture
plus Sysdig Inspect provide forensic mechanisms. Use Docker-explorer for offline
containers, and use Kubectl Sysdig Capture to trigger system events. Cloud Logging
stores Firewall rules but not data access rules by default

### Custom IAM roles
* custom roles can be applied at org or project level not at a folder level
* Service accounts have keys associated with them. A sevice account can have upto 10 keys associated with it.

### Application default credentials
* checks for presence of a google application credentials env variable
* checks default service account ( default sa is associated with compute engine, kubernetes engine and cloudfunctions)
* if 1 and 2 are not found, throws an error.
