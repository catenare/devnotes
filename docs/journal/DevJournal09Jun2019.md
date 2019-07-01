# Saturday 08 June 2019

- Creating a dynamic component loader

* `ng new dynamic-tutorial --enableIvy=true --style=scss`
* Add a new module - `ng g module dynamic-form`
* add a new component - `ng g component dynamic-form/containers/dynamic-form -m=dynamic-form`

# Sunday 09 June 2019

- Creating form components
- `ng g componenent dynamic-form/components/form-input`
- `ng g directive dynamic-form/components/dynamic-field`

* Shipping systems
* Online service couriers. Bulky equipment
* Installation services.
* Accounting integration
* After sales experience.

* LetsEncrypt - https://letsencrypt.org - Free ssl certificate
* Cloudinary - https://cloudinary.com - Image management
* ManageWP - https://managewp.com - backup and update your wordpress site
* South Africa fullfillment and ecommerce delivery services

  - UAfrica - https://www.uafrica.com/features - Have a shipping only option
  - ParcelNinja - https://www.parcelninja.com/delivery.html - Integrate with multiple services
  - http://www.ideliver-fulfillment.co.za/fulfillmentServices.asp
  - On The Dot - https://www.onthedot.co.za/e-commerce/
  - Article about different companies - https://webs.co.za/blog/itemlist/category/35-south-african-ecommerce-courier.html

  - https://wumdrop.com
  - https://pargo.co.za/about-us/

## Creating a new kinderAdmin application

- `ng new kinderAdmin --createApplication=false --enableIvy=true --routing=true --style=scss`
- `git remote add origin git@personal:catenare/kinderAppAdmin.git`

* `ng generate application sysAdmin --enableIvy=true --routing=true --style=scss`
* `ng g library schemaForm`
* `ng g component components/form-input --project schemaForm --style=scss --prefix=schema --entryComponent=true`
* `ng g component components/form-select --project schemaForm --style=scss --prefix=schema --entryComponent=true`
* `ng g component components/form-button --project schemaForm --style=scss --prefix=schema --entryComponent=true`
* `ng g directive form-field --project=schemaForm --prefix=schema --export=true`
