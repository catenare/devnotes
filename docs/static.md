# Creating a static page
* Using [foundation from zurb](http://foundation.zurb.com/)
## Setting up
1. Install foundation-cli - `npm install --global foundation-cli`
1. Create new project - `foundation new`
    * Use `foundation-zurb-template`
1. Install building block - `foundation kits install news`
## Resources
* [Placement Images List](https://www.hanselman.com/blog/TheInternetsBestPlaceholderImageSitesForWebDevelopment.aspx)
    * [Hold It](http://www.placehold.it)

## Notes
### Zurb Panini Notes
* Partials are your friends. 
    * Inserting values into partions ```{{>partion value="value"}}```
    * Use `{{#each}}` to iterate over array data
    * Use `filename.variable` to access data from file in data folder

