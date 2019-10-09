
# Lesson 0: Configuring your computer

Before the lessons, you will set up a Python computing environment for scientific computing. There are two main ways people set up Python for scientific computing.
1. By downloading and installing package by package with tools like [apt-get](https://help.ubuntu.com/community/AptGet/Howto), [pip](https://docs.python.org/3/installing/), etc.
2. By downloading and installing a Python distribution that contains binaries of many of the scientific packages needed. The major distributions of these are [Anaconda](https://www.anaconda.com) and [Enthought Canopy](https://www.enthought.com/product/canopy/). Both contain IDEs.

We recommend to use Anconda, with its associated package manager, `conda`, or Miniconda,  It has become the de facto package manager/distribution for scientific use.

Before we get rolling with the Anaconda distribution, we have some considerations and installations to get out of the way first.

## Windows users: Install Chrome or Firefox

We will be using [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/) in the Python sessions. It is browser-based, and Chrome, Firefox, and Safari are supported. Internet Explorer is **not**. Therefore, if you are a Windows user, you need to be sure you have either Chrome of Firefox installed.

## Downloading and installing Anaconda

Downloading and installing Anaconda is simple. 
1. Go to the [Anaconda distribution homepage](https://www.anaconda.com/distribution/) and download the graphical installer.  
2. Be sure to download Anaconda for Python 3.6 or 3.7 for the appropriate operating system.
3. Follow the on-screen instructions for installation. When prompted, be sure to "Install for me only."
4. You may be prompted for optional installations, like [PyCharm](https://www.jetbrains.com/pycharm/). You will not need these for this sessions. 

That's it!  After you do that, you will have a functioning Python distribution.

## Launching JupyterLab and a terminal

After installing the Anaconda distribution, you should be able to launch the **Anaconda Navigator**. If you're using macOS, this is available in your `Applications` menu. If you are using Windows, you can do this from the Start menu. Launch Anaconda Navigator.

We will be using JupyterLab throughout the Python sessions. You should see an option to launch JupyterLab. When you do that, a new browser window or tab will open with JupyterLab running. Within the JupyterLab window, you will have the option to launch a notebook, a console, a terminal, or a text editor. We will use all of these during the bootcamp. For the updating and installation of necessary packages, click on `Terminal` to launch a terminal. You will get a terminal window (probably black) with a bash prompt. We refer to this text interface in the terminal as the **command line**.

## The conda package manager

conda is a package manager for keeping all of your packages up-to-date.  It has plenty of functionality beyond our basic usage in class, which you can learn more about by reading the [docs](http://conda.pydata.org/docs/get-started.html).  We will primarily be using conda to install and update packages.

conda works from the command line.  Now that you know how to get a command line prompt, you can start using conda.  The first thing we'll do is update the packages that came with the Anaconda distribution.  To do this, enter the following on the command line:

    conda update --all

If anything is out of date, you will be prompted to perform the updates, and press `y` to continue. (If everything is up to date, you will just see a list of all the installed packages.)  They may even be some downgrades.  This happens when there are package conflicts where one package requires an earlier version of another.  conda is very smart and figures all of this out for you, so you can almost always say "yes" (or "`y`") to conda when it prompts you.

## Installations

There are several additional installations you need to do for the bootcamp. We will first install some plotting packages we need, which are available as [PyViz](http://pyviz.org).

    conda install -c pyviz pyviz
    
Some packages may again be downgraded with the installation of PyViz, and that is ok. Next, to configure JupyterLab, we need to install [node.js](https://nodejs.org/).

    conda install nodejs 
    
We will also install [watermark](https://github.com/rasbt/watermark), which enables us to conveniently display version numbers of the software we are using. For this installation, we will use `pip`. There are a few other packages from pip we will need for the bootcamp, so we can go ahead and install those now.

    pip install watermark black blackcellmagic bokeh-catplot bootcamp_utils

Finally, we need to configure JupyterLab to work with the plotting packages we will use.

    jupyter labextension install --no-build @pyviz/jupyterlab_pyviz
    
You may also wish to install a spell-checker (this one isn't necessary).

    jupyter labextension install --no-build @ijmbarr/jupyterlab_spellchecker

After installing all of these extensions, you can rebuild JupyterLab.

    jupyter lab build
    
You should close your JupyterLab session and terminate Anaconda Navigator after you have completed the build. Relaunch Anaconda Navigator and launch a fresh JupyterLab instance. As before, after JupyterLab launches, launch a new terminal window so that you can proceed with setting up Git.

## Checking your distribution
We'll now run a quick test to make sure things are working properly.  We will make a quick plot that requires some of the scientific libraries we will use in the bootcamp.

Use the JupyterLab launcher (you can get a new launcher by clicking on the `+` icon on the left pane of your JupyterLab window) to launch a notebook. In the first cell (the box next to the `In [ ]:` prompt), paste the code below. To run the code, press `Shift+Enter` while the cursor is active inside the cell. You should see a plot that looks like the one below. If you do, you have a functioning Python environment for scientific computing!


```python
import numpy as np
import bokeh.plotting
import bokeh.io

bokeh.io.output_notebook()

# Generate plotting values
t = np.linspace(0, 2*np.pi, 200)
x = 16 * np.sin(t)**3
y = 13 * np.cos(t) - 5 * np.cos(2*t) - 2 * np.cos(3*t) - np.cos(4*t)

p = bokeh.plotting.figure(height=250, width=275)
p.line(x, y, color='red', line_width=3)
text = bokeh.models.Label(x=0, y=0, text='bootcamp', text_align='center')
p.add_layout(text)

bokeh.io.show(p)
```



    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1001">Loading BokehJS ...</span>
    </div>











  <div class="bk-root" id="ba43a15e-2f3c-4dc5-9067-88abbc78be51" data-root-id="1002"></div>





## Computing environment


```python
%load_ext watermark
%watermark -v -p numpy,bokeh,jupyterlab
```

    CPython 3.7.3
    IPython 7.1.1
    
    numpy 1.16.4
    bokeh 1.2.0
    jupyterlab 0.35.5
