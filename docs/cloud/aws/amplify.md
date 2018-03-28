# Amazon Mobile Hub

## Why
* Get
  * Authentication and user management
  * Hosting including https access
  * NoSQL database
  * S3 storage (userfiles)
  * Amazon Analytics and messaging.


## Setup
1. Create User in IAM with access Keys
1. Access **AWS Mobile Hub**
1. Create a project
  1. Click *Web*
  1. Click *Start*
1. Add project title
1. Edit your region

### Setup your local environment
1. `npm install -g awsmobile-cli`
  1. `awsmobile configure aws` - set your access keys
1. Change into your project folder
1. Initialize your project
  1. `awsmobile init e32a`

### Add additional Services
1. *User Sign-in*
  1. *Email and Password*
  1. *Optional* - user required to sign in
1. *NoSQL Database*
1. *User Data Storage*

1. Update your local environment
  1. `awsmobile pull` in your project directory
