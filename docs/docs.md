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

## Setup
1. Make virtual environment for python - `mkvirtualenv -a . docsdirectory`
1. Install requirements - `pip install mkdocs pymdown-extensions pygments mkdocs-material`
1. Create mkdocs project - `mkdocs new <project>`
1. Enter into the project
1. Edit the *mkdocs.yml* file

## Using
* `mkdocs serve` - local development server *http:\\localhost:8000*
* `mkdocs gh-deploy` - build docs and push to gh-pages repo in github after committing.

## Config file - *mkdocs.yml*
```yaml
site_name: Development Notes for Johan Martin
repo_url: https://github.com/catenare/devnotes
site_description: Notes tracking for developing different apps.
site_author: Johan Martin (http://www.johan-martin.com)
repo_name: 'GitHub'
edit_uri: edit/master/md/
# docs_dir: 'md'
# site_dir: 'docs'
copyright: Johan Martin &copy; 2017
markdown_extensions:
  - pymdownx.tilde
theme: 'material'
pages:
- Home: 'index.md'
- Section:
  - 'Page Sites': 'page.md'
  - Section: 
      - sub1: 'sub1.md'
      - sub2: 'sub2.md'
```
## MkDocs Notes
* [Documentation](http://www.mkdocs.org/)
* [Github](https://github.com/mkdocs/mkdocs/)
* added ```pymdownx.tilde``` extension to get strikethrough to work.
* Using ```mkdocs gh-deploy``` to upload docs.
* Additional setup notes
    * [Squidfunk - material theme](http://squidfunk.github.io/mkdocs-material/getting-started/)

## Installing Markdown Extensions
* [PyMdown Extensions Documentation](http://facelessuser.github.io/pymdown-extensions/)
* Installation: `pip install pymdown-extensions`
* Using:
    - *pymdownx.tilde*
    - *markdown.extensions.def_list*

## Fixing Issues with MkDocs
404 error for home page/front page - github gh-pages hosting.
:   *Seems like the home page has to point to an "index.md" page for it to work.*

## Importing docs into Github
* [ghp-import](https://github.com/davisp/ghp-import)
* Already being used by MkDocs.
* Would like to use with Sphinx if I convert my documentation to Sphinx.
