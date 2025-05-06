# Role assumption CTF

This lab requires you to either use the AWS CLI locally or through AWS CloudShell.

To begin this lab, make note of the number you have been provided for your lab. Now use this to assume the role 
cross-account-# replacing # with the number of your lab (e.g. 1-10).

Your task is to assume your role in the account using the external id "Google2025".

Once you have assumed the role, you should find out what permissions your role has, and use those to gain access to further privileges. Ultimately granting you access to some data. 



Some setup hints:
To verify you've correctly assumed the role, you can use aws sts-get-caller-identity.

If you want to edit the AWS CLI Config, you can modify the default configuration file ~/.aws/config:

[profile <profile_name>]
role_arn = arn:aws:iam::555503665675:role/cross-account-#
source_profile = default
external_id = Google2025

The configuration above will associate the assume-role directly with a profile. --profile parameter can be provided with any CLI command to specify which profile you intend to use.

Once you've assumed the role, you should start by inspecting your own permissions. Do you notice any permission that will allow you to elevate privileges further?


Once you've reached the objective, you will find new IAM credentials. We can save these for later.