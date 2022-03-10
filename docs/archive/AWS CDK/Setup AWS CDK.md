# Setup AWS CDK
## Resources
* https://github.com/projen/projen - project generator. Includes generators for CDK
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
## Workshop

