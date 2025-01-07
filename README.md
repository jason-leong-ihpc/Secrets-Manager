# Secrets-Manager

## Answer the following:
### What is needed to authorize your EC2 to retrieve secrets from the AWS Secret Manager?
For an EC2 to retrieve secrets from the AWS Secrets Manager, it will need to be assigned an IAM role with the appropriate policy to access the secret.
### Derive the IAM policy (i.e. JSON)?
A sample IAM policy that [allows read access to specific secrets in AWS Secrets Manager](https://docs.aws.amazon.com/mediaconnect/latest/ug/iam-policy-examples-asm-secrets.html#iam-policy-examples-asm-specific-secrets) is listed below:
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
                "${aws_secretsmanager_secret.sample_secret.arn}"
            ]
        },
        {
            "Effect": "Allow",
            "Action": "secretsmanager:ListSecrets",
            "Resource": "arn:aws:secretsmanager:${var.region}:${var.account_id}:*"
        }
    ]
}
```
In this example, the policy will allow the EC2 to ```ListSecrets``` in a specified region and AWS account and ```GetResourcePolicy```, ```GetSecretValue```, ```DescribeSecret``` and ```ListSecretVersionIds``` for the secret of interest only.
### Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access
For a secret named ```prod/cart-service/credentials```, the ARN would be in the format:   
```arn:aws:secretsmanager:${var.region}:${var.account_id}:prod/cart-service/credentials-*```

Source: [IAM policy examples for secrets in AWS Secrets Manager](https://docs.aws.amazon.com/mediaconnect/latest/ug/iam-policy-examples-asm-secrets.html)
