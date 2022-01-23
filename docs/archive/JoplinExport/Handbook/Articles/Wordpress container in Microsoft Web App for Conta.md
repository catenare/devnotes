---
title: Wordpress container in Microsoft Web App for Containers
updated: 2020-03-01 18:38:28Z
created: 2020-02-29 12:47:15Z
---

# Wordpress container in Microsoft Web App for Containers
Transfer my current Wordpress configuration to Microsoft's app service.
1. Code is in github
2. Use pipeline to pull the code into Microsoft container registry
3. Build the container
4. Deploy to Web app container service
## Use azure cli locally
	`docker run -it mcr.microsoft.com/azure-cli`
## Code pipeline to pull code from GitHub and build
### Need the GitHub authorisation key to build the code.
* Create a devops instance on azure
	* https://dev.azure.com/
* Install the GitHub app for azure - https://github.com/apps/azure-pipelines
* Create pipeline for a Docker image
## Setup Azure Container Registry
* Use docker image for azure cli 