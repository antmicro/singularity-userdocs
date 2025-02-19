# Singularity User Docs

This project uses <a href="http://docutils.sourceforge.net/rst.html">
reStructured Text (RST)</a> and <a href="https://readthedocs.org/">ReadTheDocs
</a> . As a library for the current theme, <a
href="https://pypi.org/project/Sphinx/" alt="PyPI">Sphinx Python library </a>
was used, using Python v. 2.7.

## Setting up an environment to contribute

First things first, you will need to install the following tools:

- <a href="https://www.python.org/download/releases/2.7/">Install Python 2.7</a>
- After that then you will need to install Sphinx:

```sh
pip install -U Sphinx
```

You're all set! after this you will only need to use your favorite editor for
RST files.

## How to edit & write RST

First of all, it is good to have an idea of some files and their functionality
into the project:

### Structure of the project

This project maintains the following structure:

1. Index.rst : contains the sections and the initial table of contents tree,
   every section is referenced by a tag next to it. (e.g. ``Quick Start
   <quick_start>``)
2. All other files, are named as the same reference tag described before, so in
   the previous example, a correspondent ``quick_start.rst`` file exists.
3. The configuration at the moment of compilation is given by the ``conf.py``
   file, some more description about this file can be found below.

### The conf.py file

This file contains the themes, extensions, variables and naming for files that
the compilation process produces. Some important elements are the following:

- ``version`` : Describes the current version (This one is a short version of
  the release)
- ``release``: Describes the current release (Complete or full version
  description. For a matter of simplicity we maintain both at the same value)

- ``html_theme``: Describes the theme to be used in the ``ReadtheDocs``
  document.
- ``html_theme_options``: Describes the options needed for configuration in the
  theme (This varies from theme to theme, so we enforce using the options for
  the ``Sphinx theme`` only.
- ``html_context``: Options related to which is the github repository and what
  name it has.
- ``html_logo``: The logo for the sidebar
- ``html_favicon``: The ``favicon`` for the entire project
- ``htmlhelp_basename``: Default name of the document generated in Latex, we
  leave all these as default values.

### Cheatsheet to get started with reStructured (RST) Text

Some hints on how to write stuff on RST are described in this section.

#### 1. Create a section/subsection/subsubsection title

Sections are all described as plain text, but have specific
notations/underlining for titles and subtitles, very similar to Markup Language.

- To create a main section title: A main section title is described as a
  surrounded text (above and below) of ``=`` characters. Like in the following
  example:

```sh
================
New Main Section
================
```

- To create a sub-section: A sub section title is described as a surrounded text
  (above and below) of ``-`` characters. Like in the following example:

```sh
---------------
New Sub section
---------------
```

- To create a sub-sub-section: A sub-sub section title is described as a text
  underlined by ``=`` characters. Like in the following example:

```sh

New sub-sub section
===================

```

- Last but not least, could happen that you would need to insert a sub-sub-sub
  section, in that case the title is described as a text underlined by ``-``
  characters. Like in the following example:

```sh
New sub-sub-sub section
-----------------------
```

#### 2. Reference sections

You might need to reference sections, for that aim you will need to first create
the reference above the title you need to reference and second to reference it
where you need the link reference. Remember that this type of references is very
different than that of hyperlinks, because at the moment of compilation, the
latex document generated will have the reference to the page in which that title
was referenced. Very cool, huh? Let's see how it works...

##### Step 1: Create the reference

To create the reference on the section you need to link, you will need to
specify a tag, allowed characters contain also ``-`` characters but they need to
be unique name tags. So for example, in the build-docker-module section we can
have something like:

```sh
.. _build-docker-module:

-------------------
build-docker-module
-------------------
```

Note that it might not be necessarily that the section is called just as the
same as the tag-name.

##### Step 2: Reference it

You can do so by following the next syntax:

The name after the ref tag could also be different, the important thing is that
the tag between the ``<`` and ``>`` is the one that belongs to the previous
given tag name. Like in the following example:

```sh
:ref:`quickstart <quick-start>`
```

You can find a lot of information about RST on <a
href="http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html">this
site</a>

### Generating HTML files from RST

This is pretty straightforward by going to the root of the project on the
command line and then do:

```sh
make html SKIPCLI=1
```

This will generate a folder called **_build** which inside will have a folder
called **html** containing all the html files you need.

### Generating PDF files from RST

This is very similar to the previous step, you will need to execute on command line:

```sh
make latexpdf SKIPCLI=1
```

with this, a new folder inside **_build** will be generated, called **latex**
and in there you can find the `pdf` file generated from `RST` (by default it is
called "ReadTheDocsTemplate.pdf").

(Additional latex files are also generated if needed.)

### Generating EPUB from RST

Very similar to the previous command, you will just need to execute on a command
line:

```sh
make epub SKIPCLI=1
```

This will generate an **epub** folder inside **_build** folder. Inside you will
find the file with an `epub` extension.

## Generating CLI docs

The Singularity CLI docs are generated using the actual code from Singularity.
To do this, we include Singularity as a submodule, and whenever a Makefile
target (like `make html`) is run, Singularity itself is compiled and used to
generate the CLI docs.

However, you might not want to compile Singularity, either because you can't on
your machine, or because you want to test out a quick change to the docs.  If
this is the case, you can skip the CLI doc generation using the `SKIPCLI`
argument.  For example, to rebuild the HTML docs without including the CLI docs,
just run `make html SKIPCLI=1`.

If Singularity has been updated and you want to synchronize the CLI docs with
the new version of Singularity, you'll have to update the submodule.  To do
this, just run:

```bash
git submodule update --remote --merge
git add vendor/src/github.com/sylabs/singularity
git commit
```

This will update the Singularity submodule to the latest version of the master branch.
