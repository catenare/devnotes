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
- Development:
  - 'Static Sites': 'static.md'
  - Database: 
      - Postgresql: 'database.md'
      - Migrations: 'dbmigrations.md'
  - Languages:
    - PHP: 'php/php.md'
    - 'Python': 'python.md'
    - 'Ruby': 'ruby.md'
  - Frameworks:
    - Spring: 'spring.md'
    - Wordpress: 'php/wordpress.md'
  - Version Control:
    - 'Git': 'git.md'
  - 'Web Development':
    - 'Front-End': 'front.md'
  - Mobile:
    - 'Mobile Dev': 'mobile.md'
- Reports: 'reporting.md'
- Research: 'research.md'
- Documentation: 'docs.md'
- Other: 'other.md'
- 'Command Line': 'cmd/cmd.md'
- 'Learning Systems': 'teach.md'
```


## Fixing Issues with MkDocs
404 error for home page/front page - github gh-pages hosting.

:   *Seems like the home page has to point to an "index.md" page for it to work.*

## Using
* `mkdocs serve` - local development server *http:\\localhost:8000*
* `mkdocs gh-deploy` - build docs and push to gh-pages repo in github after committing.

## Importing docs into Github
* [ghp-import](https://github.com/davisp/ghp-import)
* Already being used by MkDocs.
* Would like to use with Sphinx if I convert my documentation to Sphinx.
