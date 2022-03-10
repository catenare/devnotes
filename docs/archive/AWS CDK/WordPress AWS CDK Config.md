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
    "UserId": "AIDAZKIVWPAYBY3IA5Y7X",
    "Account": "640532510768",
    "Arn": "arn:aws:iam::640532510768:user/nziswanodeveloper"
}
```
	* Get your default region
		* `aws configure get region --profile default`
		* Response: `eu-central-1`
	* Bootstrap your CDK stack
		`cdk bootstrap aws://640532510768/eu-central-1`
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
### Build our registry config
* `git checkout -b aws_ecr_config`
* Update our *README.md* file
