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
