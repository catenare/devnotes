# Learning About PipENV
## Resources
* [Pipenv Docs](https://docs.pipenv.org/)
* Tutorials
    * [Hitchhikers Guide - Pipenv](http://docs.python-guide.org/en/latest/dev/virtualenvs/)
    * [Packaging with Pipenv](https://code.tutsplus.com/tutorials/revisiting-python-packaging-with-pipenv--cms-30297)
    * [Managing Dependencies](https://packaging.python.org/tutorials/managing-dependencies/) - Python.org - packaging

## Notes
* `pip install --user pipenv` - installs in user mode.
* `pipenv shell` - activate the virtual environment
* Convert my **virtualenvwrapper** project to **pipenv** project.
    * CD into directory of project.
    * `pipenv install` - will install packages from **requirements.txt** file.
    * `pipenv shell` - launch the virtual environment
    * Edit **pidfile** to update dependencies to '*'.
    * `pipenv update` - update to latest packages.
* Generate a requirements file
  * `pipenv lock -r`
  * `pipenv lock -r --dev` - only the dev requirement
# Python Packages

## Database
* [SQLAlchemy](https://www.sqlalchemy.org)
* [SQLAlchemy Utils](https://sqlalchemy-utils.readthedocs.io/en/latest/#)
    * Custom datatypes and utility functions for SQLAlchemy. Inludes UUIDType.
* [psycopg](http://initd.org/psycopg/) - PostgreSQL Python Adapter

## Configuration
* [everett](https://github.com/willkg/everett) - [docs](https://everett.readthedocs.io/en/latest/)
    * Works with .env and ini files.

## Other
* [openpyxl](https://openpyxl.readthedocs.io/en/default/)
    * Library to read and write Excel files including latest Excel files.
* [click](http://click.pocoo.org/6/) - Command line library for Python.
* Microsoft Word Merge Docs
    * [docx-mailmerge](https://github.com/Bouke/docx-mailmerge)
        * [Populating MS Word Templates with Python](http://pbpython.com/python-word-template.html)
    * [python-docx](https://python-docx.readthedocs.io/en/latest/)
        * [Automate The Boring Stuff](https://automatetheboringstuff.com/chapter13/)

## Testing
* ~~[Nose](http://nose.readthedocs.io/en/latest/) - Testing for python~~
* [PyTest](https://docs.pytest.org/en/latest/)
* [Tavern](https://taverntesting.github.io/) - API testing

## Documentation
* [Mkdocs](http://www.mkdocs.org)
    * Generate documentation for project and allows you to deploy to *github gh-pages*

# Python Research and Resources
## Packages
* [Awesome Sphinx](https://github.com/yoloseem/awesome-sphinxdoc)
