# Creating Project Documentation
## Using [MkDocs](http://www.mkdocs.org/)
* Uses markdown.
* Works with github pages.
* Every project will have their own documentation
    * Styleguide should be included (frontend)
    * Project goals and requirements
    * Notes about development
    * Setup/install instructions
    * Resolution to issues (ongoing FAQ for the projects)
* Documentation pages stay in gh-pages branch.
* added ```pymdownx.tilde``` extension to get strikethrough to work.
* Using ```mkdocs gh-deploy``` to upload docs.

## MkDocs Notes
* [Documentation](http://www.mkdocs.org/)
* [Github](https://github.com/mkdocs/mkdocs/)

## Installing Markdown Extensions
* [PyMdown Extensions Documentation](http://facelessuser.github.io/pymdown-extensions/)
* Installation: `pip install pymdown-extensions`
* Using:
    - *pymdownx.tilde*
    - *markdown.extensions.def_list*

## Fixing Issues with MkDocs
404 error for home page/front page - github gh-pages hosting.

:   *Seems like the home page has to point to an "index.md" page for it to work.*

## Using
* `mkdocs serve` - local development server *http:\\localhost:8000*
* `mkdocs gh-deploy` - build docs and push to gh-pages repo in github after committing.
