# WordPress AWS CDK Config using TDD
## Details/prerequisites
* Using typescript
* AWS Account
* AWS CLI
* Visual Studio Code
* DevContainer for CodeSpaces/Docker based development on Raspberry PI
* Node.js - We use the latest lts version installed

## Setup
* Install the AWS CDK
	* `nom install -g aws-cdk` - Global install of the cod
* Bootstrap the AWS CDK - Creates the S3 bucket for your AWS account
	* Get your account details
		* `aws sts get-caller-identity --profile default` - Will show your account credentials
```
{
    "UserId": "AIDABCDEFPAYBY3IXXXXX",
    "Account": "7804444519999",
    "Arn": "arn:aws:iam::640532519999:user/nziswanodeveloper"
}
```
	* Get your default region
		* `aws configure get region --profile default`
		* Response: `eu-central-1`
	* Bootstrap your CDK stack
		`cdk bootstrap aws://78044451999/eu-central-1`
## Create the app
* Create a new repository in GitHub
	* Name: aws_wordpress_cdk
	* **Do not include a README or a .gitignore file. CDK will not run in a non-empty directory**
* Checkout the repository locally
	* `git clone git@github.com:Nziswano/aws_wordpress_cdk.git`
* `nvm use --lts` - make sure we're using the latest lts version
* `cdk init app --language typescript` - Create the CDK app
* In the cloned folder
	* Add *.nvmrc* file. Which version of node we're going to be using
		* `echo "lts/*" >> .nvmrc `
	* Add *.devcontainer* folder. CodeSpaces/Docker container for our environment
		* `cp -r ../holding_folder/.devcontainer .`
* Helpful Commands
```
## Useful commands

* `npm run build`   compile typescript to js
* `npm run watch`   watch for changes and compile
* `npm run test`    perform the jest unit tests
* `cdk deploy`      deploy this stack to your default AWS account/region
* `cdk diff`        compare deployed stack with current state
* `cdk synth`       emits the synthesized CloudFormation template
```
* Build your initial stack `npm run build`
* Verify that it worked `cdk ls` - should show your stack
* Add/update your *README.md* file
* Commit and push to GitHub.
## Building our App
### AWS Registry configuration
* API Documentation: https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_ecr-readme.html
* `git checkout -b aws_ecr_config`
* Update our *README.md* file
#### Our first stack
* `lib/aws_wordpress_cdk-stack.ts`
```typescript
import * as cdk from 'aws-cdk-lib';
import { Stack, StackProps } from 'aws-cdk-lib';
import * as ecr from 'aws-cdk-lib/aws-ecr';
import { Construct } from 'constructs';

export class AwsWordpressCdkStack extends Stack {
  constructor(scope: Construct, id: string, props?: StackProps) {
    super(scope, id, props);

    const ecr_repo = new ecr.Repository(this, 'WordpressDockerRegistry', {
      repositoryName: 'wordpress-cms-ecr',
    });
  }
}
```
##### Our Test
* File: `test/aws_wordpress_cdk.test.ts`
```typescript
import * as cdk from 'aws-cdk-lib';
import { Template } from 'aws-cdk-lib/assertions';
import * as AwsWordpressCdk from '../lib/aws_wordpress_cdk-stack';

test('WordPress Registry Created', () => {
    const app = new cdk.App();
    const stack = new AwsWordpressCdk.AwsWordpressCdkStack(app, 'MyTestStack');
    const template = Template.fromStack(stack);

    template.hasResourceProperties('AWS::ECR::Repository', {
        RepositoryName: 'wordpress-cms-ecr'
    });
});

```
* To run tests: `npm run build && cdk synth && npm run test`
#### GitHub Actions for continues integration/deployment
* Github Actions
	* https://github.com/marketplace/actions/aws-cdk-github-actions

* Environment variables - Actions secrets
	* DEV_AWS_ACCESS_KEY_ID
	* DEV_AWS_SECRET_ACCESS_KEY
	* DEV_AWS_REGION
Available to private repositories
* Setup the local environment
* Build and test
* Run the deployment
