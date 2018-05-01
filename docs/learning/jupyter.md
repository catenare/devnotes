# Jupyter Notebook
* [Jupyter](http://jupyter.org)
* Install
    * `pipenv install jupyter`

## Resources
* [JupyterLab](http://jupyterlab.readthedocs.io/en/stable/) - Extends Jupyter.
* [Jupyter Kernels](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)
* [IPython Cookbook](http://ipython-books.github.io)
* [Widgets](https://ipywidgets.readthedocs.io/en/latest/index.html)
* [Jupyter Widgets](https://github.com/jupyter-widgets)

## Notes
* Configuration - **~/Library/Jupyter**

## Installing the notebook - using pipenv
* Create notebook folder and cd into directory `mkdir notebook` 
* Install jupyter - `pipenv install jupyter`
* Install Kernels
    * Need **node.js** ,**npm** and **zeromq* installed
        * Using *macports* - `sudo port install zmq` - zeromq
        * Using **nvm** for node.js
    * Init a *package.json* file
    * Install JavaScript kernel - install everything local in folder - [GitHub](https://github.com/n-riesco/ijavascript)
        * `pipenv install pyzmq`
        * `npm install -g ijavascript` - Need to install as global for it to work correctly
        * `npx ijsinstall`
        * `npx ijsnotebook` - Run the notebook with JavaScript enabled
    * Install TypeScript kernel - [GitHub](https://github.com/nearbydelta/itypescript)
        * `npm install itypescript`
        * `jupyter notebook` - Typescript is now enabled.
    * Install Ruby - [GitHub](https://github.com/SciRuby/iruby)
        * Using **RVM** to manage Ruby
        * Install iRuby - `gem install iruby`
        * Install ffi-rzmq - `gem install ffi-rzmq`
        * `iruby register --force`
    * Install Elm - [Elm](https://github.com/abingham/jupyter-elm-kernel)
        * `pipenv install elm_kernel`
        * `python -m elm_kernel.install`
* Setting up *JuperLab* - [JupyterLab](http://jupyterlab.readthedocs.io/en/stable/index.html)
    * Install in jupyter folder - `pipenv jupyterlab`

## [BeakerX](http://beakerx.com) - includes a number of kernel extensions including SQL
* `pip install beakerx` then `beakerx install`
* Other Resources
    * [Binder](https://mybinder.org/v2/gh/twosigma/beakerx/0.15.2?filepath=StartHere.ipynb) - Notebooks with documentation for BeakerX
* Very limited documentation.
