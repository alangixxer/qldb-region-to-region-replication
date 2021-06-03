# qldb-region-to-region-replication

[![N|Solid](https://d1.awsstatic.com/r2018/h/99Product-Page-Diagram_AWS-Quantum.f03953678ba33a2d1b12aee6ee530e45507e7ac9.png)](https://aws.amazon.com/qldb/)

**WARNING**: This guide is for demonstration purposes only and should only be used in a development or test AWS environment. Elevated IAM privileges are used.

### Region Selection

This demo can be deployed in any AWS region that supports the following services:

- Amazon QLDB
- AWS Lambda
- AWS SQS
- AWS CloudFormation
- AWS Kinesis

You can refer to the [region table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) in the AWS documentation to see which regions have the supported services.


## Implementation Instructions

Each of the following sections provides an implementation overview and detailed, step-by-step instructions.

### 1. Launch CloudFormation template for primary region.

Launch one of these AWS CloudFormation templates in the Region of your choice.

Region| Launch
------|-----
US East (N. Virginia) | [Launch in us-east-1](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateUrl=https%3A%2F%2Fqldb-streaming-lab-us-east-1.s3.amazonaws.com%2Fdev%2Fcfn_templates%2Fqldb-dr-primary-region.yml&stackName=qldb-region-to-region&param_KinesisStreamName=RegionStream&param_QLDBLedgerName=region-to-region&param_ReplicationRegion=us-east-2)

### 2. Fill out the CloudFormation parameters.

Keep as default.

### 3. Launch CloudFormation template for secondary region.

Region| Launch
------|-----
US East (Ohio) | [Launch in us-east-2](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/quickcreate?templateUrl=https%3A%2F%2Fqldb-streaming-lab-us-east-2.s3.amazonaws.com%2Fdev%2Fcfn_templates%2Fqldb-dr-secondary-region.yml&stackName=qldb-region-to-region&param_KinesisStreamName=RegionStream&param_QLDBLedgerName=region-to-region)

### 4. Fill out the CloudFormation parameters.

Keep as default.

### 5. Simulate data into primary qldb ledger.

https://github.com/alangixxer/qldb-simulation-tool can be used. For high TPS configurations, additional kinesis shards will be needed.

Ensure that the QLDB Ledger name is chagned from "default" to the correct Ledger name.
