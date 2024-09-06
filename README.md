# Cfngoat - Vulnerable Cloudformation Template
[![Maintained by Bridgecrew.io](https://img.shields.io/badge/maintained%20by-bridgecrew.io-blueviolet)](https://bridgecrew.io/?utm_source=github&utm_medium=organic_oss&utm_campaign=cfngoat)
[![Infrastructure Tests](https://www.bridgecrew.cloud/badges/github/bridgecrewio/cfngoat/general)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=bridgecrewio%2Fcfngoat&benchmark=INFRASTRUCTURE+SECURITY)
[![CIS AWS](https://www.bridgecrew.cloud/badges/github/bridgecrewio/cfngoat/cis_aws)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=bridgecrewio%2Fcfngoat&benchmark=CIS+AWS+V1.2)
[![PCI-DSS](https://www.bridgecrew.cloud/badges/github/bridgecrewio/cfngoat/pci)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=bridgecrewio%2Fcfngoat&benchmark=PCI-DSS+V3.2)
[![SOC2](https://www.bridgecrew.cloud/badges/github/bridgecrewio/cfngoat/soc2)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=bridgecrewio%2Fcfngoat&benchmark=SOC2)
[![ISO](https://www.bridgecrew.cloud/badges/github/bridgecrewio/cfngoat/iso)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=bridgecrewio%2Fcfngoat&benchmark=ISO27001)
[![NIST-800-53](https://www.bridgecrew.cloud/badges/github/bridgecrewio/cfngoat/nist)](https://www.bridgecrew.cloud/link/badge?vcs=github&fullRepo=bridgecrewio%2Fcfngoat&benchmark=NIST-800-53)
[![slack-community](https://img.shields.io/badge/Slack-4A154B?style=plastic&logo=slack&logoColor=white)](https://slack.bridgecrew.io/)


Cfngoat is one  of Bridgecrew's "Vulnerable by Design" Infrastructure as Code repositories, a learning and training project that demonstrates how common configuration errors can find their way into production cloud environments.

![Cfngoat](.github/cfngoat-removebg-preview.png)

It's an ideal companion to testing build time Infrastructure as Code scanning tools, such as [Bridgecrew](https://bridgecrew.io/) & [Checkov](https://checkov.io) 

## Table of Contents

* [Introduction](#introduction)
* [Installation](#Installation)
* [Contributing](#contributing)
* [Support](#support)

## IaC Optional input reference

directory: example/
file: example/tfplan.json # optional: provide the path for resource to be scanned. This will override the directory if both are provided.
quiet: true # optional: display only failed checks
soft_fail: true # optional: do not return an error code if there are failed checks
framework: terraform # optional: run only on a specific infrastructure {cloudformation,terraform,kubernetes,all}
skip_framework: terraform # optional: skip a specific infrastructure {cloudformation,terraform,kubernetes,all}
output_format: sarif # optional: the output format, one of: cli, json, junitxml, github_failed_only, or sarif. Default: sarif
output_file_path: reports/results.sarif # folder and name of results file
baseline: cloudformation/.checkov.baseline # optional: Path to a generated baseline file. Will only report results not in the baseline.

## Introduction

Cfngoat was built to enable DevSecOps design and implement a sustainable misconfiguration prevention strategy. It can be used to test a policy-as-code framework like  [Bridgecrew](https://bridgecrew.io/?utm_source=github&utm_medium=organic_oss&utm_campaign=cfngoat) & [Checkov](https://github.com/bridgecrewio/checkov/), inline-linters, pre-commit hooks or other code scanning methods.

Cfngoat follows the tradition of existing *Goat projects that provide a baseline training ground to practice implementing secure development best practices for cloud infrastructure.


## Installation
 
```bash
aws cloudformation create-stack --stack-name cfngoat --template-body file://cfngoat.yaml --region us-east-1 --parameters ParameterKey=Password,ParameterValue=MyPassword10 --capabilities CAPABILITY_NAMED_IAM
```

Expect provisioning to take at least 5 minutes.  

Multiple stacks can be deployed simultaniously by changing the `--stack-name` and adding an `Environment` parameter:

```bash
aws cloudformation create-stack --stack-name cfngoat2 --template-body file://cfngoat.yaml --region us-east-1 --parameters ParameterKey=Password,ParameterValue=MyPassword10 ParameterKey=Environment,ParameterValue=dev2 --capabilities CAPABILITY_NAMED_IAM
```

## Important notes

* **Where to get help:** the [Bridgecrew Community Slack](https://slack.bridgecrew.io/?utm_source=github&utm_medium=organic_oss&utm_campaign=cfngoat)

Before you proceed please take a not of these warning:
> :warning: Cfngoat creates intentionally vulnerable AWS resources into your account. **DO NOT deploy Cfngoat in a production environment or alongside any sensitive AWS resources.**

## Requirements

* aws cli


## Bridgecrew's IaC herd of goats

* [CfnGoat](https://github.com/bridgecrewio/cfngoat) - Vulnerable by design Cloudformation template
* [TerraGoat](https://github.com/bridgecrewio/terragoat) - Vulnerable by design Terraform stack
* [CDKGoat](https://github.com/bridgecrewio/cdkgoat) - Vulnerable by design CDK application

## Contributing

Contribution is welcomed!

We would love to hear about more ideas on how to find vulnerable infrastructure-as-code design patterns.

## Support

[Bridgecrew](https://bridgecrew.io/?utm_source=github&utm_medium=organic_oss&utm_campaign=cfngoat) builds and maintains Cfngoat to encourage the adoption of policy-as-code.

If you need direct support you can contact us at [info@bridgecrew.io](mailto:info@bridgecrew.io).

## Existing vulnerabilities (Auto-Generated)

|    | check_id    | file          | resource                                  | check_name                                                                                                                                                                                               | guideline                                                                                                                    |
|----|-------------|---------------|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|  0 | CKV_AWS_46  | /cfngoat.yaml | AWS::EC2::Instance.EC2Instance            | Ensure no hard-coded secrets exist in EC2 user data                                                                                                                                                      | https://docs.bridgecrew.io/docs/bc_aws_secrets_1                                                                             |
|  1 | CKV_AWS_3   | /cfngoat.yaml | AWS::EC2::Volume.WebHostStorage           | Ensure all data stored in the EBS is securely encrypted                                                                                                                                                  | https://docs.bridgecrew.io/docs/general_3-encrypt-eps-volume                                                                 |
|  2 | CKV_AWS_24  | /cfngoat.yaml | AWS::EC2::SecurityGroup.WebNodeSG         | Ensure no security groups allow ingress from 0.0.0.0:0 to port 22                                                                                                                                        | https://docs.bridgecrew.io/docs/networking_1-port-security                                                                   |
|  3 | CKV_AWS_23  | /cfngoat.yaml | AWS::EC2::SecurityGroup.WebNodeSG         | Ensure every security groups rule has a description                                                                                                                                                      | https://docs.bridgecrew.io/docs/networking_31                                                                                |
|  4 | CKV_AWS_18  | /cfngoat.yaml | AWS::S3::Bucket.FlowBucket                | Ensure the S3 bucket has access logging enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/s3_13-enable-logging                                                                         |
|  5 | CKV_AWS_21  | /cfngoat.yaml | AWS::S3::Bucket.FlowBucket                | Ensure the S3 bucket has versioning enabled                                                                                                                                                              | https://docs.bridgecrew.io/docs/s3_16-enable-versioning                                                                      |
|  6 | CKV_AWS_53  | /cfngoat.yaml | AWS::S3::Bucket.FlowBucket                | Ensure S3 bucket has block public ACLS enabled                                                                                                                                                           | https://docs.bridgecrew.io/docs/bc_aws_s3_19                                                                                 |
|  7 | CKV_AWS_55  | /cfngoat.yaml | AWS::S3::Bucket.FlowBucket                | Ensure S3 bucket has ignore public ACLs enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/bc_aws_s3_21                                                                                 |
|  8 | CKV_AWS_19  | /cfngoat.yaml | AWS::S3::Bucket.FlowBucket                | Ensure the S3 bucket has server-side-encryption enabled                                                                                                                                                  | https://docs.bridgecrew.io/docs/s3_14-data-encrypted-at-rest                                                                 |
|  9 | CKV_AWS_56  | /cfngoat.yaml | AWS::S3::Bucket.FlowBucket                | Ensure S3 bucket has 'restrict_public_bucket' enabled                                                                                                                                                    | https://docs.bridgecrew.io/docs/bc_aws_s3_22                                                                                 |
| 10 | CKV_AWS_54  | /cfngoat.yaml | AWS::S3::Bucket.FlowBucket                | Ensure S3 bucket has block public policy enabled                                                                                                                                                         | https://docs.bridgecrew.io/docs/bc_aws_s3_20                                                                                 |
| 11 | CKV_AWS_107 | /cfngoat.yaml | AWS::IAM::Policy.UserPolicy               | Ensure IAM policies does not allow credentials exposure                                                                                                                                                  | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-credentials-exposure                                        |
| 12 | CKV_AWS_111 | /cfngoat.yaml | AWS::IAM::Policy.UserPolicy               | Ensure IAM policies does not allow write access without constraints                                                                                                                                      | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-write-access-without-constraint                             |
| 13 | CKV_AWS_108 | /cfngoat.yaml | AWS::IAM::Policy.UserPolicy               | Ensure IAM policies does not allow data exfiltration                                                                                                                                                     | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-data-exfiltration                                           |
| 14 | CKV_AWS_109 | /cfngoat.yaml | AWS::IAM::Policy.UserPolicy               | Ensure IAM policies does not allow permissions management without constraints                                                                                                                            | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-permissions-management-resource-exposure-without-constraint |
| 15 | CKV_AWS_40  | /cfngoat.yaml | AWS::IAM::Policy.UserPolicy               | Ensure IAM policies are attached only to groups or roles (Reducing access management complexity may in-turn reduce opportunity for a principal to inadvertently receive or retain excessive privileges.) | https://docs.bridgecrew.io/docs/iam_16-iam-policy-privileges-1                                                               |
| 16 | CKV_AWS_110 | /cfngoat.yaml | AWS::IAM::Policy.UserPolicy               | Ensure IAM policies does not allow privilege escalation                                                                                                                                                  | https://docs.bridgecrew.io/docs/ensure-iam-policies-does-not-allow-privilege-escalation                                      |
| 17 | CKV_AWS_7   | /cfngoat.yaml | AWS::KMS::Key.LogsKey                     | Ensure rotation for customer created CMKs is enabled                                                                                                                                                     | https://docs.bridgecrew.io/docs/logging_8                                                                                    |
| 18 | CKV_AWS_16  | /cfngoat.yaml | AWS::RDS::DBInstance.DefaultDB            | Ensure all data stored in the RDS is securely encrypted at rest                                                                                                                                          | https://docs.bridgecrew.io/docs/general_4                                                                                    |
| 19 | CKV_AWS_157 | /cfngoat.yaml | AWS::RDS::DBInstance.DefaultDB            | Ensure that RDS instances have Multi-AZ enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/general_73                                                                                   |
| 20 | CKV_AWS_17  | /cfngoat.yaml | AWS::RDS::DBInstance.DefaultDB            | Ensure all data stored in RDS is not publicly accessible                                                                                                                                                 | https://docs.bridgecrew.io/docs/public_2                                                                                     |
| 21 | CKV_AWS_23  | /cfngoat.yaml | AWS::EC2::SecurityGroup.DefaultSG         | Ensure every security groups rule has a description                                                                                                                                                      | https://docs.bridgecrew.io/docs/networking_31                                                                                |
| 22 | CKV_AWS_107 | /cfngoat.yaml | AWS::IAM::Policy.EC2Policy                | Ensure IAM policies does not allow credentials exposure                                                                                                                                                  | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-credentials-exposure                                        |
| 23 | CKV_AWS_111 | /cfngoat.yaml | AWS::IAM::Policy.EC2Policy                | Ensure IAM policies does not allow write access without constraints                                                                                                                                      | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-write-access-without-constraint                             |
| 24 | CKV_AWS_108 | /cfngoat.yaml | AWS::IAM::Policy.EC2Policy                | Ensure IAM policies does not allow data exfiltration                                                                                                                                                     | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-data-exfiltration                                           |
| 25 | CKV_AWS_109 | /cfngoat.yaml | AWS::IAM::Policy.EC2Policy                | Ensure IAM policies does not allow permissions management without constraints                                                                                                                            | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-permissions-management-resource-exposure-without-constraint |
| 26 | CKV_AWS_116 | /cfngoat.yaml | AWS::Lambda::Function.AnalysisLambda      | Ensure that AWS Lambda function is configured for a Dead Letter Queue(DLQ)                                                                                                                               | https://docs.bridgecrew.io/docs/ensure-that-aws-lambda-function-is-configured-for-a-dead-letter-queue-dlq                    |
| 27 | CKV_AWS_173 | /cfngoat.yaml | AWS::Lambda::Function.AnalysisLambda      | Check encryption settings for Lambda environmental variable                                                                                                                                              | https://docs.bridgecrew.io/docs/bc_aws_serverless_5                                                                          |
| 28 | CKV_AWS_45  | /cfngoat.yaml | AWS::Lambda::Function.AnalysisLambda      | Ensure no hard-coded secrets exist in lambda environment                                                                                                                                                 | https://docs.bridgecrew.io/docs/bc_aws_secrets_3                                                                             |
| 29 | CKV_AWS_18  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure the S3 bucket has access logging enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/s3_13-enable-logging                                                                         |
| 30 | CKV_AWS_20  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure the S3 bucket does not allow READ permissions to everyone                                                                                                                                         | https://docs.bridgecrew.io/docs/s3_1-acl-read-permissions-everyone                                                           |
| 31 | CKV_AWS_21  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure the S3 bucket has versioning enabled                                                                                                                                                              | https://docs.bridgecrew.io/docs/s3_16-enable-versioning                                                                      |
| 32 | CKV_AWS_53  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure S3 bucket has block public ACLS enabled                                                                                                                                                           | https://docs.bridgecrew.io/docs/bc_aws_s3_19                                                                                 |
| 33 | CKV_AWS_55  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure S3 bucket has ignore public ACLs enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/bc_aws_s3_21                                                                                 |
| 34 | CKV_AWS_19  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure the S3 bucket has server-side-encryption enabled                                                                                                                                                  | https://docs.bridgecrew.io/docs/s3_14-data-encrypted-at-rest                                                                 |
| 35 | CKV_AWS_56  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure S3 bucket has 'restrict_public_bucket' enabled                                                                                                                                                    | https://docs.bridgecrew.io/docs/bc_aws_s3_22                                                                                 |
| 36 | CKV_AWS_54  | /cfngoat.yaml | AWS::S3::Bucket.DataBucket                | Ensure S3 bucket has block public policy enabled                                                                                                                                                         | https://docs.bridgecrew.io/docs/bc_aws_s3_20                                                                                 |
| 37 | CKV_AWS_18  | /cfngoat.yaml | AWS::S3::Bucket.FinancialsBucket          | Ensure the S3 bucket has access logging enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/s3_13-enable-logging                                                                         |
| 38 | CKV_AWS_21  | /cfngoat.yaml | AWS::S3::Bucket.FinancialsBucket          | Ensure the S3 bucket has versioning enabled                                                                                                                                                              | https://docs.bridgecrew.io/docs/s3_16-enable-versioning                                                                      |
| 39 | CKV_AWS_53  | /cfngoat.yaml | AWS::S3::Bucket.FinancialsBucket          | Ensure S3 bucket has block public ACLS enabled                                                                                                                                                           | https://docs.bridgecrew.io/docs/bc_aws_s3_19                                                                                 |
| 40 | CKV_AWS_55  | /cfngoat.yaml | AWS::S3::Bucket.FinancialsBucket          | Ensure S3 bucket has ignore public ACLs enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/bc_aws_s3_21                                                                                 |
| 41 | CKV_AWS_19  | /cfngoat.yaml | AWS::S3::Bucket.FinancialsBucket          | Ensure the S3 bucket has server-side-encryption enabled                                                                                                                                                  | https://docs.bridgecrew.io/docs/s3_14-data-encrypted-at-rest                                                                 |
| 42 | CKV_AWS_56  | /cfngoat.yaml | AWS::S3::Bucket.FinancialsBucket          | Ensure S3 bucket has 'restrict_public_bucket' enabled                                                                                                                                                    | https://docs.bridgecrew.io/docs/bc_aws_s3_22                                                                                 |
| 43 | CKV_AWS_54  | /cfngoat.yaml | AWS::S3::Bucket.FinancialsBucket          | Ensure S3 bucket has block public policy enabled                                                                                                                                                         | https://docs.bridgecrew.io/docs/bc_aws_s3_20                                                                                 |
| 44 | CKV_AWS_18  | /cfngoat.yaml | AWS::S3::Bucket.OperationsBucket          | Ensure the S3 bucket has access logging enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/s3_13-enable-logging                                                                         |
| 45 | CKV_AWS_53  | /cfngoat.yaml | AWS::S3::Bucket.OperationsBucket          | Ensure S3 bucket has block public ACLS enabled                                                                                                                                                           | https://docs.bridgecrew.io/docs/bc_aws_s3_19                                                                                 |
| 46 | CKV_AWS_55  | /cfngoat.yaml | AWS::S3::Bucket.OperationsBucket          | Ensure S3 bucket has ignore public ACLs enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/bc_aws_s3_21                                                                                 |
| 47 | CKV_AWS_19  | /cfngoat.yaml | AWS::S3::Bucket.OperationsBucket          | Ensure the S3 bucket has server-side-encryption enabled                                                                                                                                                  | https://docs.bridgecrew.io/docs/s3_14-data-encrypted-at-rest                                                                 |
| 48 | CKV_AWS_56  | /cfngoat.yaml | AWS::S3::Bucket.OperationsBucket          | Ensure S3 bucket has 'restrict_public_bucket' enabled                                                                                                                                                    | https://docs.bridgecrew.io/docs/bc_aws_s3_22                                                                                 |
| 49 | CKV_AWS_54  | /cfngoat.yaml | AWS::S3::Bucket.OperationsBucket          | Ensure S3 bucket has block public policy enabled                                                                                                                                                         | https://docs.bridgecrew.io/docs/bc_aws_s3_20                                                                                 |
| 50 | CKV_AWS_53  | /cfngoat.yaml | AWS::S3::Bucket.DataScienceBucket         | Ensure S3 bucket has block public ACLS enabled                                                                                                                                                           | https://docs.bridgecrew.io/docs/bc_aws_s3_19                                                                                 |
| 51 | CKV_AWS_55  | /cfngoat.yaml | AWS::S3::Bucket.DataScienceBucket         | Ensure S3 bucket has ignore public ACLs enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/bc_aws_s3_21                                                                                 |
| 52 | CKV_AWS_19  | /cfngoat.yaml | AWS::S3::Bucket.DataScienceBucket         | Ensure the S3 bucket has server-side-encryption enabled                                                                                                                                                  | https://docs.bridgecrew.io/docs/s3_14-data-encrypted-at-rest                                                                 |
| 53 | CKV_AWS_56  | /cfngoat.yaml | AWS::S3::Bucket.DataScienceBucket         | Ensure S3 bucket has 'restrict_public_bucket' enabled                                                                                                                                                    | https://docs.bridgecrew.io/docs/bc_aws_s3_22                                                                                 |
| 54 | CKV_AWS_54  | /cfngoat.yaml | AWS::S3::Bucket.DataScienceBucket         | Ensure S3 bucket has block public policy enabled                                                                                                                                                         | https://docs.bridgecrew.io/docs/bc_aws_s3_20                                                                                 |
| 55 | CKV_AWS_18  | /cfngoat.yaml | AWS::S3::Bucket.LogsBucket                | Ensure the S3 bucket has access logging enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/s3_13-enable-logging                                                                         |
| 56 | CKV_AWS_53  | /cfngoat.yaml | AWS::S3::Bucket.LogsBucket                | Ensure S3 bucket has block public ACLS enabled                                                                                                                                                           | https://docs.bridgecrew.io/docs/bc_aws_s3_19                                                                                 |
| 57 | CKV_AWS_55  | /cfngoat.yaml | AWS::S3::Bucket.LogsBucket                | Ensure S3 bucket has ignore public ACLs enabled                                                                                                                                                          | https://docs.bridgecrew.io/docs/bc_aws_s3_21                                                                                 |
| 58 | CKV_AWS_56  | /cfngoat.yaml | AWS::S3::Bucket.LogsBucket                | Ensure S3 bucket has 'restrict_public_bucket' enabled                                                                                                                                                    | https://docs.bridgecrew.io/docs/bc_aws_s3_22                                                                                 |
| 59 | CKV_AWS_54  | /cfngoat.yaml | AWS::S3::Bucket.LogsBucket                | Ensure S3 bucket has block public policy enabled                                                                                                                                                         | https://docs.bridgecrew.io/docs/bc_aws_s3_20                                                                                 |
| 60 | CKV_AWS_111 | /cfngoat.yaml | AWS::IAM::Role.CleanupRole                | Ensure IAM policies does not allow write access without constraints                                                                                                                                      | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-write-access-without-constraint                             |
| 61 | CKV_AWS_108 | /cfngoat.yaml | AWS::IAM::Role.CleanupRole                | Ensure IAM policies does not allow data exfiltration                                                                                                                                                     | https://docs.bridgecrew.io/docs/ensure-iam-policies-do-not-allow-data-exfiltration                                           |
| 62 | CKV_AWS_116 | /cfngoat.yaml | AWS::Lambda::Function.CleanBucketFunction | Ensure that AWS Lambda function is configured for a Dead Letter Queue(DLQ)                                                                                                                               | https://docs.bridgecrew.io/docs/ensure-that-aws-lambda-function-is-configured-for-a-dead-letter-queue-dlq                    |
| 63 | CKV_AWS_58  | /eks.yaml     | AWS::EKS::Cluster.EKSCluster              | Ensure EKS Cluster has Secrets Encryption Enabled                                                                                                                                                        | https://docs.bridgecrew.io/docs/bc_aws_kubernetes_3                                                                          |


---


|    | check_id     | file          | resource                                 | check_name                 | guideline                                     |
|----|--------------|---------------|------------------------------------------|----------------------------|-----------------------------------------------|
|  0 | CKV_SECRET_2 | /cfngoat.yaml | 25910f981e85ca04baf359199dd0bd4a3ae738b6 | AWS Access Key             | https://docs.bridgecrew.io/docs/git_secrets_2 |
|  1 | CKV_SECRET_6 | /cfngoat.yaml | d70eab08607a4d05faa2d0d6647206599e9abc65 | Base64 High Entropy String | https://docs.bridgecrew.io/docs/git_secrets_6 |


---


