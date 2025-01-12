# AWS EC2 and Secrets Manager Authorization

## 1. What is needed to authorize your EC2 to retrieve secrets from the AWS Secrets Manager?

### Requirements to Authorize EC2 to Retrieve Secrets

To authorize an EC2 instance to retrieve secrets from AWS Secrets Manager:

1. **Attach an IAM role to the EC2 instance:**

- The EC2 instance must be associated with an IAM role.
- This role should have an attached policy granting access to the specific secrets.

2. **IAM Policy:**

- The IAM policy should include permissions for the `secretsmanager:GetSecretValue` action.
- The policy should restrict access to the specific secret resource.

3. **Trust Relationship:**

- The IAM role must include a trust relationship that allows the EC2 service to assume the role.

## 2. IAM Policy JSON

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "secretsmanager:GetSecretValue",
      "Resource": "arn:aws:secretsmanager:<region>:<account-id>:secret:prod/cart-service/credentials"
    }
  ]
}
```

## 3. Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access

- arn:aws:secretsmanager:<region>:<account-id>:secret:prod/cart-service/credentials
