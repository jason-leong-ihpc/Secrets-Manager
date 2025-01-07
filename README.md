# Secrets-Manager

## Answer the following:
### What is needed to authorize your EC2 to retrieve secrets from the AWS Secret Manager?
For an EC2 to retrieve secrets from the AWS Secrets Manager, it will need to be assigned an IAM role with the appropriate policy to access the secret.
### Derive the IAM policy (i.e. JSON)?
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "secretsmanager:GetResourcePolicy",
                "secretsmanager:GetSecretValue",
                "secretsmanager:DescribeSecret",
                "secretsmanager:ListSecretVersionIds"
            ],
            "Resource": [
                "arn:aws:secretsmanager:us-west-2:111122223333:secret:aes128-1a2b3c",
                "arn:aws:secretsmanager:us-west-2:111122223333:secret:aes192-4D5e6F",
                "arn:aws:secretsmanager:us-west-2:111122223333:secret:aes256-7g8H9i"
            ]
        },
        {
            "Effect": "Allow",
            "Action": "secretsmanager:ListSecrets",
            "Resource": "*"
        }
    ]
} 
```
### Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access

Source: [IAM policy examples for secrets in AWS Secrets Manager](https://docs.aws.amazon.com/mediaconnect/latest/ug/iam-policy-examples-asm-secrets.html)
