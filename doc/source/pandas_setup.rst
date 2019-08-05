======================================
Before the sprint: Set up instructions
======================================

Make sure you **bring your own laptop** to the sprint.

You need the next software installed:

* Git
* An editor (vim, emacs, PyCharm,...). Make sure the editor is set up to use 4 spaces for tabs.

The `pandas contributing guide <https://pandas.pydata.org/pandas-docs/stable/contributing.html>`_
contains detailed instructions on how to set up a pandas development environment.
This document is a short summary with some additional information specific to
the sprint.

.. note::
    The steps below will download around 900Mb for the pandas repository, and
    around 600Mb for Anaconda from the Internet. If you don't have access to a
    fast Internet connection, contact your local chapter organizer, who will
    try to get a copy of both on a usb key.

.. note::
    **Windows users:** `Video tutorial: Set up pandas development environment
    in Windows <https://www.youtube.com/watch?v=417zAcfM96U>`_ by Frank Akogun.
    
Instructions
------------

1. Create a GitHub account
~~~~~~~~~~~~~~~~~~~~~~~~~~

If you don't have a GitHub account yet, simply go to https://github.com/join,
and provide your personal information (name, email...). Select the free plan.

2. Get the pandas source code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All the changes during the sprints need to be made to the latest development
version of pandas in a Git repository. Do not make them to a version downloaded
from the Internet via pip, conda or a zip.

Follow these steps to get the latest development version:

Fork the `pandas repository <https://github.com/pandas-dev/pandas>`_ on GitHub
by clicking the `Fork` button on the top-right

.. note::
    **Windows users**: run the next commands in a Git Bash session in the
    directory where you want to download pandas source code (download `Git for
    Windows <https://gitforwindows.org/>`_ if needed).

In the terminal of your computer, in the directory where you want the copy of
pandas source code, run: ::

    git clone https://github.com/<your-github-username>/pandas

or (if you have set up SSH keys for accessing GitHub): ::

    git clone git@github.com:<your-github-username>/pandas

This will create a directory named ``pandas``, containing the latest version of
the source code. We will name this directory ``<pandas-dir>`` in the rest of
this document.

Make sure you're in the root of the ``<pandas-dir>`` directory. ::

    cd <pandas-dir>

Then, set the upstream remote, so you can fetch the updates from the pandas
repository: ::

    git remote add upstream https://github.com/pandas-dev/pandas

or (if you have set up SSH keys for accessing GitHub): ::

    git remote add upstream git@github.com:pandas-dev/pandas

To fetch the latest updates from the pandas repository, follow the steps in
`Syncing a Fork <https://help.github.com/articles/syncing-a-fork/>`_: ::

    git fetch upstream
    git checkout master
    git merge upstream/master


3. Set up a Python environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Download and install `Anaconda <https://www.anaconda.com/download/>`_.

  .. note::
    **Windows users**: run the next commands in the Anaconda Prompt (found in the Anaconda
    folder of the Start menu).

* Activate conda in one of the following ways (or equivalent, if you know what
  you're doing):

    * If you chose to prepend Anaconda to your PATH during install adding it to
      your ``~/.bashrc``, just restart your terminal.
    * Otherwise, run ``export PATH="<path-to-anaconda>/bin:$PATH"`` in your
      terminal. Keep in mind that it will be active exclusively in the terminal
      you run this command.

* Create a conda environment: ::

    conda env create -n pandas_dev -f <path-to-pandas-dir>/environment.yaml

  .. note::
    **Windows users**: If you're copy-pasting the path, replace all pasted
    ``\`` characters with ``/`` for the command to work.

* Activate the new conda environment: ::

    source activate pandas_dev

* Install pandas development dependencies: ::

    conda install -c defaults -c conda-forge --file=<path-to-pandas-dir>/requirements-dev.txt

4. Compile C code in pandas
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Besides the Python `.py` files, pandas source code includes C/Cython files
which need to be compiled in order to run the development version of pandas.

.. note::
    **Windows users**: to compile pandas, you need to install `Visual Studio
    2017 <https://www.visualstudio.com/>`_. You need Visual Studio Community
    2017 (2.5GB download during installation) as a minimum. Visual Studio Code
    does not support the required Build Tools and will not work.

    Select the workload "Python development" and the option "Python native
    development tools" on the right side.

    Users of legacy Python 2.7 should install `Microsoft Visual C++ Compiler
    for Python 2.7 <https://www.microsoft.com/download/details.aspx?id=44266>`_
    instead.
    
    After the installation, run the following commands in Anaconda Prompt.

To compile these files simply run: ::

    cd <pandas-dir>
    python setup.py build_ext --inplace

The process will take several minutes.

5. Create a branch and start coding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

On the day of the sprint, you will get assigned one pandas function or method
to work on. Once you know which, you need to create a git branch for your
changes. This will be useful when you have finished your changes, and you want
to submit a pull request, so they are included in pandas.

.. note::
   **Windows users**: run the next commands with Git Bash started in the cloned
   pandas folder.

Before creating a branch, make sure that you fetched the latest master version
of the upstream pandas repository. You can do this with: ::

    git checkout master
    git pull upstream master --ff-only

Then, you can create a new git branch running: ::

    git checkout -b <new_branch_name>

The branch name should be descriptive of the feature you will work on. For
example, if you will work on the docstring of the method ``head``, you can
name your branch ``docstring_head``.

If during the sprint you work in more than one docstring, you will need a
branch for each.

To check in which branch are you: ::

    git branch

To change to another branch: ::

    git checkout <branch_name>
