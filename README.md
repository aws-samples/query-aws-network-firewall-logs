# Query AWS Network Firewall Logs in a few clicks

Observability is an important aspect of security. Security services and solutions generate logs and it is imperative to have a mechanism to query the logs. This simple Cloudformation template deploys a mechanism to query AWS Network Firewall logs in a few clicks. This can improve the MTTR (mean time to respond) to a security event.

## Pre-requisite

* Preconfigured AWS Network Firewall with S3 Bucket log destination.
* IAM Permissions to deploy Cloudformation resources

## Tech Stack

* AWS CLI
* CloudFormation stack
* Amazon Athena Named Query
* AWS Glue Data Catalog table

## Deployment Steps

1. Download the Cloudformation template into the current working directory
2. Copy and paste the following command into your terminal - be sure to change the parameters to your actual values.

   ```bash
   aws cloudformation create-stack --stack-name *some-stack* --template-body file://query-aws-network-firewall-logs.yml --parameters ParameterKey=AthenaNamedQueryName,ParameterValue=*some-query* ParameterKey=LogBucketName,ParameterValue=*some-bucket* ParameterKey=TableName,ParameterValue=*some-table*
   ```

3. The command should return a *stack id* which signifies a successful execution.

## How to run the query in Amazon Athena

1. From the AWS management console, navigate to **Amazon Athena**
2. In the Athena console, select **Saved Queries** and select the query you deployed in the previous step.
3. Click **Run**
4. In the left pane of the page, you should see a new *AwsDataCatalog* table with the name you provided show up.
5. Click on the ellipsis next to the table name and select **preview table**
6. That's it, you are ready to query the network logs!

## Clean up

1. In your shell terminal, run the following command. 
  
   ```bash
   aws cloudformation delete-stack --stack-name *some-stack*
   ```

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
