# Developer Notebook for [Johan Martin](mailto:martin.johan@johan-martin.com)
## Notes are online at [Johan Martin's Development Notes](http://devnotes.johan-martin.com/)
* Easier to write things down then trying to remember what you forgot.
* Working on web development projects is changing rapidly and constantly.
* Resources are available everywhere but some are outdated and only some help with solving your problem.
* Easier to review notes on how you solved it last time than googling and going through all the articles again.
* Too much Googling can lead to a waste of time.
* Track your development
## Tech
* Notes are written in Markdown
	* Using [IA Writer](https://ia.net/writer/) and Microsoft Visual Studio Code to edit the docs.
* Site generated with [MkDocs](http://www.mkdocs.org/)
	* Deciding factor was the ability to push docs to *gh-pages* on Github.
	* Essentially free hosting for my document notebook.
* Notes for setting up notebook in notebook.

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
* Use pipenv
1. Create project directory and *CD* into it
1. Install mkdocs as dev dependency - `pipenv install mkdocs --dev`
1. Create mkdocs direcotry - `mkdocs new sitedocs`
* *sitedocs\docs* is where the markdown goes.
* *sitedocs\mkdocs.yml* - your table of contents.

## Using
* `mkdocs serve` - local development server *http://localhost:8000*
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
    * `pipenv install mkdocs-material --dev`

## Installing Markdown Extensions
* [PyMdown Extensions Documentation](http://facelessuser.github.io/pymdown-extensions/)
* Installation: `pipenv install pymdown-extensions --dev`
* Using:
    - *pymdownx.tilde*
    - *markdown.extensions.def_list*

## Fixing Issues with MkDocs
* 404 error for home page/front page - github gh-pages hosting.: *Seems like the home page has to point to an "index.md" page for it to work.*
* RuntimeError: Click will abort further execution because Python 3 was configured to use ASCII as encoding for the environment.  Consult http://click.pocoo.org/python3/for mitigation steps.
* Fix with:
    * `> export LC_ALL=en_US.UTF-8`
    * `> export LANG=en_US.UTF-8`

## Importing docs into Github
* [ghp-import](https://github.com/davisp/ghp-import)
* Already being used by MkDocs.
* Would like to use with Sphinx if I convert my documentation to Sphinx.

## Updates
* Updated notes about WordPress CLI
* 24 April 2018 - Added API section. PHP, Python, Node.js frameworks related creating APIs.
		* Added notes about **pipenv**
* 25 April 2018 - Added Jupyter notebook with support for TypeScript, JavaScript and Ruby.

### Monday 13 April 2020
* Refactor documents to simplify and make relevant.
* Topics
	* Cloud
		* AWS
		* Azure
		* Google
			* Firebase
		* Others
			* Cloudinary
	* Web Development
	* Tools
	* Resources
