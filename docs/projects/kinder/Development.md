# Getting started on the new version of KinderCare

## Notes

- Setup for git since I'm working with multiple git repositories.

```
[remote "origin"]
        url = git@personal:catenare/kinderAdmin.git
[user]
        email = martin.johan@catenare.co.za
        name = Johan Martin
```

## Pipfile upgrade for docs

- Changed the pipfile version to latest version of python
- Ran `pipenv update` to upgrade everything
- Removed _requirements.txt_ since it was giving an vulnerability alert

## Setting up Angular for my application

- Generate a new application - `ng new kinderApp --style=scss --routing=true`
- Add angular material design - `ng add @angular/material`
- Add progressive web app - `ng add @angular/pwa`
- Add to github. Customize because I have multiple configurations for git. `git remote add origin git@personal:catenare/kinderApp.git`

## Creating first module

- Generate module `ng generate module center --project=kinderApp --routing=true`
- Generate component `ng generate component center/info --module=center --selector=center-detail`
- Now have the basics for this module

* Using angular material schematics with angular cli - `https://material.angular.io/guide/schematics`
* Generate a new dashboard for the center - `ng generate @angular/material:dashboard center/dashboard --module=center`
* Generate a sidenav using material design - `ng generate @angular/material:nav center/sidenav --module=center`

## End of day notes

- Let's tie this all into our main app. Need to be able to get the dashboard
- Ended up using clarity for my basic layout. Able to get it to look like something. [Clarity Design](https://clarity.design/). Documentation is limited. Totally using by accident. Might change later.
- Using routing to access the center module. Got that to work.
  - routing module in center module has link/route to center home page.
  - Access the route int he main/app routing module using loadChildren and pointing to the center module. Makes it a litte cleaner.
  - Now need to actually build out the site. Still thinking through how it is suppose to function. More complex than initially planned.
  # Wednesday 24 April 2019
  - Need to choose a json-schema to use for generating a form
  - json api serializer - [ngx-jsonapi](https://github.com/reyesoft/ngx-jsonapi)
  - json schema form generator - [json-schema-form](https://github.com/hamzahamidi/Angular6-json-schema-form)
