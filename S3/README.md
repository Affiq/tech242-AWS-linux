
## Installing AWSCLI
We will first need to install the AWS CLI package so that we can communicate with AWS, done with the following command. You may add the -y flag and non debian interactive flag if you wish to bypass user input:
```sudo apt install awscli```
```non-interactive install```

We can verify the install using ```aws --version```, with which an output (which also verifies python version) confirms the installation.

## AWSCLI Configuration
After the installation, we will need 4 pieces of information:
* Access Key (may have to ask admin)
* Secret Access Key (may have to ask admin)
* Region (we will ``use eu-west-1``)
* Message format (we will use ``json``)

We will then use ```aws configure``` and enter the corresponding details from above.

## S3 Bucket Commands
```aws s3 help``` Lists all available aws s3 commands

```aws s3 mb s3://<bucket-name>``` To create a bucket

```aws s3 ls``` List all buckets in organisations S3

```aws s3 ls s3://<bucket-name> ``` List all files in a bucket

```aws s3 cp <filename> s3://<bucket-name>``` Copy file into a bucket

```aws s3 rm s3://<bucket-name-file-path>``` Delete file from bucket

```aws s3 rb s3://tech242-affiq-first-bucket``` Remove a bucket (provided it is empty)
```aws s3 rb s3://tech242-affiq-first-bucket --force``` Remove a bucket and all files inside

## Make S3-File Public
Go to S3 console and navigate to your bucket.
1. Go to Permissions and change public access
2. Go to Permissions and Enable ACL
3. Navigate to Objects and click the checkbox for <File-To-Publicise> and select ```Actions > Make Public Using ACL```



