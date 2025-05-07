# Assessing AWS with Prowler

For this lab, we will use open-source version of Prowler to get an overview of our AWS estate. [Prowler](https://docs.prowler.com/projects/prowler-open-source/en/latest/) is a Python-based package for scanning AWS configuration.

We will run this for the account "o3c-goat", where you have been granted the AWSSecurityAssessor role through AWS SSO. This role consists of the two managed policies:
- SecurityAudit
- ViewOnlyAccess
And the following custom policy:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "account:Get*",
                "appstream:Describe*",
                "appstream:List*",
                "backup:List*",
                "backup:Get*",
                "bedrock:List*",
                "bedrock:Get*",
                "cloudtrail:GetInsightSelectors",
                "codeartifact:List*",
                "codebuild:BatchGet*",
                "codebuild:ListReportGroups",
                "cognito-idp:GetUserPoolMfaConfig",
                "dlm:Get*",
                "drs:Describe*",
                "ds:Get*",
                "ds:Describe*",
                "ds:List*",
                "dynamodb:GetResourcePolicy",
                "ec2:GetEbsEncryptionByDefault",
                "ec2:GetSnapshotBlockPublicAccessState",
                "ec2:GetInstanceMetadataDefaults",
                "ecr:Describe*",
                "ecr:GetRegistryScanningConfiguration",
                "elasticfilesystem:DescribeBackupPolicy",
                "glue:GetConnections",
                "glue:GetSecurityConfiguration*",
                "glue:SearchTables",
                "glue:GetMLTransforms",
                "lambda:GetFunction*",
                "logs:FilterLogEvents",
                "lightsail:GetRelationalDatabases",
                "macie2:GetMacieSession",
                "macie2:GetAutomatedDiscoveryConfiguration",
                "s3:GetAccountPublicAccessBlock",
                "shield:DescribeProtection",
                "shield:GetSubscriptionState",
                "securityhub:BatchImportFindings",
                "securityhub:GetFindings",
                "servicecatalog:Describe*",
                "servicecatalog:List*",
                "ssm:GetDocument",
                "ssm-incidents:List*",
                "states:ListTagsForResource",
                "support:Describe*",
                "tag:GetTagKeys",
                "wellarchitected:List*"
            ],
            "Resource": "*",
            "Effect": "Allow",
            "Sid": "AllowMoreReadOnly"
        },
        {
            "Effect": "Allow",
            "Action": [
                "apigateway:GET"
            ],
            "Resource": [
                "arn:*:apigateway:*::/restapis/*",
                "arn:*:apigateway:*::/apis/*"
            ],
            "Sid": "AllowAPIGatewayReadOnly"
        }
    ]
}
```

Notice that AWS Managed Policies for viewing all configuration data isn't accurate, relying on these will result in "blind spots" when you are assessing AWS environments.

Before running Prowler, make sure to set the environment variables that can be found in the AWS Identity Center:
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...
export AWS_SESSION_TOKEN="..

These credentials will now take precedence over the instance profile.



### Running in your EC2 instance
Python 3.9 comes preinstalled on your EC2 instance. If your performing the lab on your EC2 instance, first make sure you have pip installed (Python Package Manager):
`python3 -m ensurepip --upgrade`

Then install Prowler in the user directory:
```
python3 -m pip install prowler --user

# Create an output directory
mkdir -p ~/prowler-output

# Run prowler with the -o parameter
python3 -m prowler aws -o ~/prowler-output
```


### Running Locally
*If you are runnng this locally, you should use a virtualenv instead with the instructions below:*
```
python3 -m virtualenv venv
. ./venv/bin/activate
pip install prowler
prowler aws
```

While Prowler runs, grab yourself a coffee! 

*If you want to view the HTML report, it's in the output folder of this directory*

** Use the AWS Console or CLI to see if your able to identify some of the findings from Prowler.**

