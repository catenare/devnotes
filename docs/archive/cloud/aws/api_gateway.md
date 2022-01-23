# Amazon API Gateway
## Setup
* Endpoint - regional since it will only be used for admin and probably only in the US. **Can be changed afterwards**
![](/images/lookfindme_api_gateway/create_api_01.png)
![](/images/lookfindme_api_gateway/create_api_02.png)
* To Do List
	- [x] Create custom domain name. It takes a while to go through the system. 
	- [x] Must have a certificate for https support. Import from Amazon Certificate Manager. Only in N.Virginia available. Next to the CIA.
		* Can't do custom domain name because current name points to another cloudfront distribution already. Will probably have to use the command line to figure out which distribution this is and how so I can go and change it.
				
	- [x] Setup Client Certificate - Try to limit the access to the backend server for API access.
![](/images/lookfindme_api_gateway/create_api_03_create_private_certificate.png)
		* Seems that the Amazon Gateway kept the certificate from the last gateway I deleted.
	
	- [x] Setup the endpoints ![](/images/lookfindme_api_gateway/create_api_04_endpoint.png)
	- [x] Will be setup as proxy services
		* admin
		* site
		* test
		* user ![](/images/lookfindme_api_gateway/create_api_05_proxies.png)
	- [x] Configure proxies for access to backend server at adminapi.lookfindme.com ![](/images/lookfindme_api_gateway/create_api_05_http_proxy_setting.png)
	- [x] Test the proxies - I normally create a hello endpoint just for basic testing. ![](/images/lookfindme_api_gateway/create_api_06_test_hello_world.png)
	- [x] Deploy API ![](/images/lookfindme_api_gateway/create_api_07_api_deployed.png)
	- [x] Setup logging ![](/images/lookfindme_api_gateway/create_api_08_stage_logging_configure.png)
    * Finding the ARN in cloudwatch logs ![](/images/lookfindme_api_gateway/create_api_08_logging_setup_arn_role.png)
  - [x] Create a custom domain name. Have to go into GoDaddy and delete that cname record.![](/images/lookfindme_api_gateway/create_api_99.png)
	- [x] Setup local environment to use correct aws credentials `aws apigateway get-domain-names --profile lookfindme`  
		* [Amazon API Gateway CLI Reference](https://docs.aws.amazon.com/cli/latest/reference/apigateway)
		
