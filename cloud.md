# TestMazzaTech

Thinking about our deployment on AWS, we have to know how much we will pay for it, as this will have a major impact on the final cost. Reading about AWS in “US-EAST-1” we can estimate approximately the price we will have, in summary,

* With a load of 10,000 page loads per minute, considering 60 minutes/hour, 24 hours/day and 30 days/month, this results in approximately 432 million requests per month.

* Cost of API calls:
5 million calls at 3.50 USD per million = 17.50 USD.

* Cost of data transfer:
Each call transfers 3 KB, totaling 14.3 GB/month. At 0.09 USD per GB, the cost is 1.29 USD.

* Total cost of Amazon API Gateway (US-EAST-1):
17.50 USD (API calls) + 1.29 USD (data transfer) = 18.79 USD/month.

This figure reflects the estimated cost of processing and transferring requests on the Amazon API Gateway, within the US-EAST-1 region.


<p>Cost Analysis for Cloud Environments</p>

Base Setup (AWS)
Component	              Service	                       Cost Estimate
      API Layer        |	AWS Fargate (ECS)	        |     $46/month for 2 vCPU, 4GB RAM (100% uptime).
    Database Layer     | 	Amazon RDS (PostgreSQL)	    |     $90/month for db.t3.medium (Multi-AZ).
    Caching Layer      | 	Amazon ElastiCache (Redis)	|     $40/month for a small node.
    Service Discovery  |	AWS App Mesh	            |     $7.20/month (for 10 active services).
    Load Balancing     |	AWS ALB	                    |     $20/month (minimal traffic).
    Object Storage     |	Amazon S3                   |     $0.023/GB for 1TB of data.




To make our lives easier, we will use AWS with Github Actions. To set it up, we have to go to AWS Management Console panel and search for IAM. Then, go to Users and create a new one, giving it a name. You need to edit the IAM Role's trust policy to reduce the scope of access to just your repository. Go back to the list of IAM Roles and select the role you created, so click on Trust Relationship, and ti must be similar with it:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Federated": "arn:aws:iam::[aws-account-id]:oidc-provider/token.actions.githubusercontent.com"
      },
      "Action": "sts:AssumeRoleWithWebIdentity",
      "Condition": {
        "StringEquals": {
          "token.actions.githubusercontent.com:aud": "sts.amazonaws.com"
        },
        "StringLike": {
          "token.actions.githubusercontent.com:sub": "repo:[nome-da-org]/[nome-do-repo]:*"
        }
      }
    }
  ]
}


The important part you must add is
"StringLike": {
  "token.actions.githubusercontent.com:sub": "repo:[nome-da-org]/[nome-do-repo]:*"
}

*For some extras infos: 
https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege



But we have to configure it in our github in the same way.  In Github, go to Settings, after that “Secrets and Variables”, and Actions. Then click on New Repository Secret and adding the following information:

on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v3
      - uses: aws-actions/setup-sam@v2
      - uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      - run: sam build --use-container
      - run: sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
	  




Go to 
 [Kubernetes](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/kubernetes.md)