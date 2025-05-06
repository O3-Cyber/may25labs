# CloudFormation Guard Lab
The purpose of this lab is to setup and test CloudFormation Guard with CloudFormation Hooks.

The template in the setup folder will prepare most of the infrastructure required, including:
* A bucket for hosting the rules
* A separate bucket where the output will be written to.
* An IAM Policy for the Cloudformation Hooks
* A service trust policy allowing the CloudFormation Hooks service to assume the role.


To complete the lab:
1. Inspect the template in the setup folder to understand how it works and deploy it.
2. Once deployed, check the s3_bucket_public_read_acl.guard file. This is the file rule you want to use.
3. Upload the rule to the new rule bucket created. Then follow the instructions for creating a cloudformation hook
4. Once the hook is deployed, try deploying the template for s3 found in this folder. 
5. You will find the output in the output bucket. See if you are able to change the template to allow it to deploy. 

Once you've configured the infrastructure, you can experiment with different rules from the [registry](https://github.com/aws-cloudformation/aws-guard-rules-registry/tree/main). 

You can also install cloudformation-guard locally to test rules, or embed it into a pipeline of your choice.

