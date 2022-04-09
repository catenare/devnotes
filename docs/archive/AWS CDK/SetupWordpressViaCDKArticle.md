# Setup AWS CDK
## Resources
* https://github.com/projen/projen - project generator. Includes generators for CDK
* Test Resources: 
	* https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.assertions-readme.html
	* https://axelhodler.medium.com/tests-for-aws-cdk-code-9a4bce9fec0e
* [Fargate with EFS and Aurora Serverless using AWS CDK](https://blog.codecentric.de/en/2021/03/fargate-with-efs-and-aurora-serverless-using-aws-cdk/)
	* WordPress with Aurora and Elastic File System
* [Building an image searching solution with the AWS CDK](https://aws.amazon.com/blogs/compute/building-an-image-searching-solution-with-the-aws-cdk/)
* [How to create an RDS Aurora serverless instance with CDK](https://dev.to/cjjenkinson/how-to-create-an-aurora-serverless-rds-instance-on-aws-with-cdk-5bb0)
## Tutorials
* [AWS CDK v2 Tutorial – How to Create a Three-Tier Serverless Application](https://www.freecodecamp.org/news/aws-cdk-v2-three-tier-serverless-application/)
* [Testing the Async Cloud with AWS CDK](https://dev.to/aws-builders/testing-the-async-cloud-with-aws-cdk-33aj)
## Details
* [Aspects](https://docs.aws.amazon.com/cdk/v2/guide/aspects.html)
## CDK Documentation 
* [ConstructHub](https://constructs.dev)
* [CDK Patterns](https://cdkpatterns.com)
* [AWS CDK API Reference](https://docs.aws.amazon.com/cdk/api/v2//docs/aws-cdk-lib.aws_ecr-readme.html)
## Setup AWS CLI environment with correct keys
* `aws configure`
	* Need:
		* AWS Access Key
		* AWS Secret Access Key
		* Default Region name: eu-central-1
		* Default output format: json
## Setup CDK environment
* `npm install -g aws-cdk`
* `cdk bootstrap`
* Be sure to import cdk `import * as cdk from 'aws-cdk-lib';`
* `cdk synth` -> `cdk deploy`
* Make changes
* `cdk diff` -> `cdk deploy`
* `cdk destroy`
## GitHub Actions
* https://github.com/marketplace/actions/aws-cdk-github-actions
* https://github.com/marketplace/actions/aws-cdk-action
* https://github.com/aws-actions

## Setup constructs

### ECR
### SSM Parameters
### Aurora Serverless MySQL
* Resources
* https://bobbyhadz.com/blog/aws-cdk-rds-example
#### Secrets Manager
* [How to create an RDS Aurora serverless instance with CDK](https://dev.to/cjjenkinson/how-to-create-an-aurora-serverless-rds-instance-on-aws-with-cdk-5bb0)
#### VPC
### API Gateway
### Fargate

Can destroy one stack at a time
* `cdk destroy CmsCdkStack`