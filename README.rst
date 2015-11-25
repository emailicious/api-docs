Emailicious API documentation
=============================

.. image:: https://travis-ci.org/emailicious/api-docs.svg?branch=master
    :target: https://travis-ci.org/emailicious/api-docs

The `Emailicious`_ API documentation is built using `Sphinx`_.

.. _`Emailicious`: https://www.emailicious.com
.. _`Sphinx`: http://sphinx-doc.org/

*****************
Building the docs
*****************

In order to build the docs you will need to install the
`required Python dependencies`_. We suggest you use ``pip`` to perform the
installation::

    pip install -r requirements.txt

Once all the required packages are installed you can simply use ``make`` to
target the desired build::

    make html

Windows user can use the provided ``make.bat`` script to perform the same
actions.

Building localized docs
"""""""""""""""""""""""

A localized version of the documentation can be built by passing the
appropriate Sphinx options as an environment variable::

    sphinx-intl build
    make html -e SPHINXOPTS="-D language='fr'" 

.. _`required Python dependencies`: https://raw.githubusercontent.com/emailicious/api-docs/master/requirements.txt

********************
Translating the docs
********************

The documentation are translated using `sphinx-intl`_ which relies on
`gettext`_ under the hood.

In order to generate the translation catalogs for a specific locale the
following commands must be run::

    make gettext
    sphinx-intl update -p build/locale -l <locale>

Where ``<locale>`` should be replaced by the name of the locale to generate
the catalogs for.

Once these command complete the translation catalogs (``.po`` files) will be
available for edition in the ``source/locale/<locale>/LC_MESSAGES`` directory.

You can proceed to `building localized docs`_.

.. _`sphinx-intl`: http://sphinx-doc.org/latest/intl.html
.. _`gettext`: http://www.gnu.org/software/gettext/manual/gettext.html#Introduction
