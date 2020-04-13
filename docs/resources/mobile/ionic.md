# Ionic Development Notes
Trying to figure out Ionic while building a prototype to demo via the web.
## Notes
* Pushing site to gh-pages.
    * Ref: [Deploying an Angular App to Github Pages](https://alligator.io/angular/deploying-angular-app-github-pages/)
    * Ionic starter template includes the manifest and worker file by default.
    * Use the ionic build scripts to create the web version of your app.
    1. Install *angular-cli-ghpages* globally
        * `npm install --global angular-cli-ghpages`
    1. Build ionic app with base-href to github gh-url for your username
        * `npm run ionic:build --prod --base-href "https://<username>.github.io/<repository>/"`
    1. Push to gh-pages. `ngh --dir www` - have to use *www* because the script looks for the *dist* folder by default.
