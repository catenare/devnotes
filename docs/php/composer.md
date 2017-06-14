# Notes about using Composer to manage a package
## Notes for managing a custom plugin with php composer.
1. Create json file in plugin directory
1. Use the **type** property as plugin. Wordpress JSON file will install it in the right location.
1. Use **dev-{branch}** to have composer checkout the correct git branch.