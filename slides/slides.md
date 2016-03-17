% Harnessing the Power of Python in ArcGIS Using the Conda Distribution
% Shaun Walbridge; Mark Janikas; Ting Lee

<section data-background="images/title.png">
<h2>[https://github.com/scw/conda-devsummit-2016-talk](https://github.com/scw/conda-devsummit-2016-talk)</h2>
<h3>[Handout PDF](https://4326.us/esri/conda/devsummit-2016-conda-arcgis-presentation-handout.pdf)</h3>
<h3>[High Quality PDF (2MB)](https://4326.us/esri/conda/devsummit-2016-conda-arcgis-presentation-full.pdf)</h3>
</section>

Conda {data-background="images/bg-1.png"}
======

Conda {data-background="images/bg-1.png"}
-----

 * Brand new: thought it was more important to show it to you than to focus on telling you about it
 * Time today to discuss your needs and what we might do to solve your problems

Why Python? ![](images/logos/Python_64x64.png){class="tight"} {data-background="images/bg-1.png"}
-----------

 - Accessible for new-comers, and the [most taught first language in US universites](http://cacm.acm.org/blogs/blog-cacm/176450-python-is-now-the-most-popular-introductory-teaching-language-at-top-us-universities/fulltext)
 - Extensive package collection (56 thousand on [PyPI](https://pypi.python.org/pypi)), broad user-base
 - Strong glue language used to bind together many environments, both open source and commercial
 - Open source with liberal license &mdash; do what you want

Package Management for Python {data-background="images/bg-1.png"}
----------------------------

Why not ``pip``, wheels, virtualenvs?

 - Don't handle the harder problem of system dependencies, considered out of scope by Python packagers --- does it end up in ``site-packages``?
 - Package devs: On OSX and Linux, 'easy' to get the deps! Use a system package manager (e.g. ``apt``, ``brew``, ``yum``) and the included compiler (e.g. ``clang``, ``gcc``).
 - It's still not easy to make reproducible builds, and what about Windows?

What about Windows? {data-background="images/bg-1.png"}
-------------------

 * We are particularly stuck on Windows which lacks broadly used package management 
    - NuGet is great, but not a system-level package manager
    - If managing applications, try [Chocolatey](https://chocolatey.org/)
 * Only devs have a C compiler on their machine
    - The essential model is compilers for few, runtimes for all
 * Package management is hard! (Except on JavaScript -- universal compilers are a leg-up)

. . .

 * Enter Conda

Why Conda? {data-background="images/bg-1.png"}
----------

![](images/logos/continuum_analytics.png){class="tight" style="width: 200px"}

* Scientific Python community identified that there was a gap not being addressed by the core Python infrastructure, limiting their ability to get packages into the hands of users

* Industry standard built by people who care about this space -- Continuum Analytics

Why Conda? {data-background="images/bg-1.png"}
----------

![](images/logos/continuum_analytics.png){class="tight" style="width: 200px"}

* It solves a hard problem:

 - Handles dependencies for many languages (C, C++, R and of course Python)
 - Built for Python first, but it really solves a much broader infrastructural issue.


Conda {data-background="images/bg-7.png"}
=====

Conda ![](images/logos/anaconda_mini.png){class="tight"} {data-background="images/bg-7.png"}
-----

 - Cross-platform: simply develop recipes for building and installing software on Linux, OS X and Windows. All it takes: a `meta.yaml`, and a build recipe.
 - Open source (BSD): Esri is using it, you can use it in your own projects for other contexts

Conda ![](images/logos/anaconda_mini.png){class="tight"} {data-background="images/bg-7.png"}
-----

What can it install?  Not just scientific packages. It can help with:

 - GUI toolkits (PyQt, TKinter)
 - C++ Libraries (Boost)
 - IDEs (Spyder, Juptyer)

See [conda-recipes](https://github.com/conda/conda-recipes/) for a comprehensive set of build recipes. Everything from applications to compilers to Python modules, hundreds of maintained recipes across many problem domains.

Conda ![](images/logos/anaconda_mini.png){class="tight"} {data-background="images/bg-7.png"}
--------------

 + Environments: Can isolate a Python environment, flexibly make changes withot affecting installed software.
 + Requirements -- include explicit state information, not just the package name. Names aren't enough!
 + Also handles platforms and Jupyter notebooks

How Does it Work? {data-background="images/bg-7.png"}
-----------------

Conda packages can come from a variety of locations:

 - On disk (``file://``)
 - Public repositories hosted on Anaconda Cloud
 - Public repositories self-hosted
 - Private repositories
 - Paid private repositories

Conda Basics {data-background="images/bg-7.png"}
------------

<div style="float: right; align: right">
![](images/hazard.png){class="tight"}
</div>
<div>
Command line interface

Will show what we're working on to make this easier, especially for non-developers

[Conda Cheatsheet](http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf)
</div>

Conda Basics {data-background="images/bg-7.png"}
------------

To start:

    conda --help

* A collection of packages and Python install is called an *environment* or *env*, the building block for managing Python with Conda
* Can have multiple environments and seamlessly switch between them

Conda Basics {data-background="images/bg-7.png"}
------------

Activating environments, a couple ways:

 * Use the shortcuts
 * Manually activate the environment:

```sh
    cd /d C:\ArcGIS\bin\Python\Scripts
    activate arcgispro-py3
```

Conda Basics {data-background="images/bg-7.png"}
------------

Once you're in an environment get details with ``info``:

    conda info

Conda info is the starting point -- it tells you the state of the environment.

Conda Basics {data-background="images/bg-7.png"}
------------

``conda info``

```
Current conda install:

             platform : win-64
        conda version : 4.0.4
  conda-build version : not installed
       python version : 3.5.1.final.0
     requests version : 2.9.1
     root environment : C:\ArcGIS\bin\Python  (writable)
  default environment : C:\ArcGIS\bin\Python\envs\arcgispro-py3
     envs directories : C:\ArcGIS\bin\Python\envs
        package cache : C:\ArcGIS\bin\Python\pkgs
         channel URLs : https://conda.anaconda.org/esri/win-64/
                        https://conda.anaconda.org/esri/noarch/
                        https://repo.continuum.io/pkgs/free/win-64/
                        https://repo.continuum.io/pkgs/free/noarch/
          config file : C:\ArcGIS\bin\Python\.condarc
``` 

Conda Basics {data-background="images/bg-7.png"}
------------

Creating new environments:

 - A few different ways. Can manually specify the dependencies:

```
    conda create --name my_env python=3.4 numpy flask dask
```
 - Can also use a file which includes all the dependencies:
```
    conda create --name my_env --file my_sweet_depends.txt
```
These can contain explcit information about channels, to ensure that 
the new environment precisely matches the requirements.

Conda vs... {data-background="images/bg-7.png"}
-----------

Name | Means | Will Ship?
-|-|-
Conda | The command itself | ✓
Miniconda | A minimum set of Python packages to build and run Conda. | ✓
Anaconda | A distribution 200+ packages built with Conda | &nbsp;
Anaconda Server | Host the full infrastructure internally | &nbsp;

Conda Demo {data-background="images/bg-7.png"}
----------

Deeper Dive {data-background="images/bg-7.png"}
===========

Conda Behind Firewall {data-background="images/bg-7.png"}
---------------------

* How's it work?

* Lock it down: Don't use network

* Can vet the installation

* Will work out of the box with default packages without any network connectivity

``.condarc``&nbsp;{data-background="images/bg-7.png"}
------------

* Modify defaults with a simple simple YAML file for configuration
* Can be updated with ``conda config``, just like using ``git config`` to update the default configuration

[A detailed example ``.condarc``](https://github.com/conda/conda/blob/ae721928109eb973b45614b790c36aca43618f65/tests/condarc)

Creating packages {data-background="images/bg-7.png"}
-----------------

Straightforward:

 * A metadata document (``meta.yaml``) specifying the contents and dependencies
 * A build command (``bld.bat``, ``build.sh``) specifying how to build

Creating packages {data-background="images/bg-7.png"}
-----------------

``meta.yaml``:

```yaml
package:
  name: pypdf2
  version: "1.25.1"

source:
  fn: PyPDF2-1.25.1.tar.gz
  url: https://pypi.python.org/packages/source/P/PyPDF2/PyPDF2-1.25.1.tar.gz
  md5: ee5e5b01d00b120805e5049e56c6fd7c

requirements:
  run:
    - python
```

Creating packages {data-background="images/bg-7.png"}
-----------------

``bld.bat``:

```sh
"%PYTHON%" setup.py install
```

Multiple Pythons {data-background="images/bg-7.png"}
----------------

Currently:

Platform | Python version
--------|--------
Desktop |  Python 2.7.x (2.7.10)
Pro | Python 3.4.x (3.4.3)

Multiple Pythons {data-background="images/bg-7.png"}
----------------

Upgrade code?  [Python migration for ArcGIS Pro](http://pro.arcgis.com/en/pro-app/arcpy/get-started/python-migration-for-arcgis-pro.htm)

 - Do it already! You can support 2 + 3 without that much work
 - If you hit an issue, it's probably because you don't understand Unicode yet -- [Watch this PyCon talk](https://www.youtube.com/watch?v=sgHbC6udIqc), _Pragmatic Unicode, or, How do I stop the pain?_

. . .

<br> 
But... this can be costly. For many organizations, a significant burden, even if the
language changes are relatively small.

Multiple Pythons with Conda {data-background="images/bg-7.png"}
---------------------------

With Conda, we can support multiple platforms:

 * Py 2.7, 3.4, 3.5 in Pro 1.3

Create a new environment, target a different Python, users can now use that with the Py2 code

Still need to change ``arcpy.mapping`` to ``arcpy.mp`` when moving from Desktop to Pro, but no Python language level changes needed.

Challenges {data-background="images/bg-7.png"}
----------

Have to make sure you're running the right Python (_what happens when you type ``python`` at the command line?_)

 - We will make this easy as possible
 - It'll be easy to tell in app
 - Isolated installation fixes a variety of issues

Requires some user education over the "only one Python on the box" model

What Do I Get Out of the Box? {data-background="images/bg-7.png"}
-----------------------------

* Conda command and a Conda root Python install
* New modules (e.g. ``requests``)
* Conda environment with all of the ArcGIS Pro dependencies as Conda packages

How can I use this? {data-background="images/bg-7.png"}
-------------------

 * We already ship you the SciPy stack -- powerful and out of the box, can use today (Pro and 10.4)
 * Can start using ``conda`` today. Miniconda is fully stand-alone, won't affect your global Python (unless you tell it to)
 * Package your work: this is an opportunity to distribute it, possibly including commercial side as well.

Where Can I Run This? {data-background="images/bg-7.png"}
---------------------

![](images/arcgis-pro-icon.png){class="tight" style="padding: 5px"}

 * ArcGIS Pro 1.3 (Release: 2016 UC)
    - Will be _the_ Python install.
    - UI for interaction

 * Future:
    - Take advantage of more features
    - Integration with platform

from future import * {data-background="images/bg-7.png"}
--------------------

Effectively manage complex software dependencies with Conda. Thousands of packages exist today, can integrate it into your organization's needs.

Resources {data-background="images/bg-7.png"}
=========

Resources {data-background="images/bg-7.png"}
--------------

[Conda Recipes](https://github.com/conda/conda-recipes)

[Anaconda.org](https://anaconda.org)

[Conda Cheatsheet](http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf)


Closing {data-background="images/bg-7.png"}
=======

Thanks {data-background="images/bg-7.png"}
------

Esri Conda Team:

![](images/conda-team.jpg){class="tight" style="width:600px"}

Continuum Analytics for creating and open sourcing Conda

Rate This Session {data-background="images/bg-7.png"}
-----------------

iOS, Android: Feedback from within the app

Windows Phone, don't use a smartphone?: Cuniform tablets accepted (sorry! limitation).

. . .

**Windows Phone, or no smartphone?** Cuneiform tablets accepted.

![](images/Amarna_Akkadian_letter_rotated_2.png){style="border: none; background: none; box-shadow: none;"}

<span style="display:none">fin</span> {data-background="images/end.png"}
---


