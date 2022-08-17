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

