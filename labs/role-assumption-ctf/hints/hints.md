Hint 1: 
You will need to list the attached role policies

Hint 2:
aws iam list-attached-role-policies --role-name cross-account-9 --profile xaccount9

Hint 3:
You need to list the policy versions before you can query the exact policy. 
aws iam list-policy-versions --policy-arn "arn:aws:iam::555503665675:policy/<policy_found_in_previous_step>" --profile <profile_name>

Hint 4: 
aws iam get-policy-version --policy-arn "arn:aws:iam::555503665675:policy/<policy_found_in_previous_step>" --version-id <version_from_previous_step> --profile <profile_name>

Hint 5: 
aws iam attach-role-policy --policy-arn arn:aws:iam::555503665675:policy/<policy_name_that_you_can_attach> --role-name cross-account-# --profile <profile_name>

Hint 6: Notice there's a permission to attach a specific policy!

Hint 7: Let's see what the new policy can do.

Hint 8:
Try listing all S3 buckets, and check out its policy. Notice the bucket is checking for the Department Attribute?

Hint 9: aws s3api get-bucket-policy --bucket <name_of_bucket_listed_starting_with_ctf> --profile <profile_name>

Hint 10: Try tagging your role and see if you can access the data.

Hint 11: aws iam tag-role --role-name cross-account-# --tags Key=Department,Value=Finance --profile <profile_name>

Hint 12: aws s3 cp s3://<bucket_name>/<file_name>> ./<dest_file_name> --profile <profile_name>