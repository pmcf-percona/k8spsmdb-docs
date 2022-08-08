# Data at rest encryption

[Data at rest encryption in Percona Server for MongoDB](https://docs.percona.com/percona-server-for-mongodb/latest/data-at-rest-encryption.html) is supported by the Operator since version 1.1.0.

**NOTE**: “Data at rest” means inactive data stored as files, database records, etc.

Following options the `mongod` section of the `deploy/cr.yaml` file should
be edited to turn this feature on:


1. The `security.enableEncryption` key should be set to `true` (the default
value).


2. The `security.encryptionCipherMode` key should specify proper cipher mode
for decryption. The value can be one of the following two variants:


    * `AES256-CBC` (the default one for the Operator and Percona Server for
MongoDB)


    * `AES256-GCM`


3. `security.encryptionKeySecret` should specify a secret object with the
encryption key:

```yaml
mongod:
  ...
  security:
    ...
    encryptionKeySecret: my-cluster-name-mongodb-encryption-key
```

Encryption key secret will be created automatically if it
doesn’t exist. If you would like to create it yourself, take into account
that [the key must be a 32 character string encoded in base64](https://docs.mongodb.com/manual/tutorial/configure-encryption/#local-key-management).