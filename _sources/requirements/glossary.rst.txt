Glossary
========

.. glossary::

   Built Distribution

      A :term:`Distribution <Distribution Package>` format containing files
      and metadata that only need to be moved to the correct location on the
      target system, to be installed.

   Distribution Package

      A versioned archive file that contains Python :term:`packages
      <Import Package>`, :term:`modules <Module>`, and other resource files
      that are used to distribute a :term:`Release`.  The archive file
      is what an end-user will download from the internet and install.

      A distribution package is more commonly referred to with the single words
      *package* or *distribution*, but this guide may use the expanded term
      when more clarity is needed to prevent confusion
      with an :term:`Import Package` (which is also commonly called a *package*)
      or another kind of distribution (e.g. a Linux distribution
      or the Python language distribution), which are often referred
      o with the single term *distribution*.

   Import Package

      A Python module which can contain other modules or recursively,
      other packages.

   The InterPlanetary File System (IPFS)

      IPFS_ is a protocol and peer-to-peer network for storing and sharing data
      in a distributed file system.  It uses content-addressing
      to uniquely identify each file in a global namespace
      connecting all computing devices.

   Module

      The basic unit of code reusability in Python.

   Package Index

      A repository of distributions with a web interface to automate
      :term:`package <Distribution Package>` discovery and consumption.

   Per Project Index

      A private or other non-canonical :term:`Package Index` indicated by
      a specific :term:`Project` as the index preferred or required to
      resolve dependencies of that project.

   Project

      A library, framework, script, plugin, application, or collection of data
      or other resources, or some combination thereof that is intended to be
      packaged into a :term:`Distribution <Distribution Package>`.

      Python projects must have unique names, which are registered on
      :term:`PyPI <Python Package Index (PyPI)>`. Each project will then
      contain one or more :term:`Releases <Release>`, and each release may
      comprise one or more :term:`distributions <Distribution Package>`.

      .. note::

         There is a strong convention to name a project after the name
         of the package that is imported to run that project.  However,
         this doesn't have to hold true.  It's possible to install
         a distribution from the project ``foo`` and have it provide
         a package importable only as ``bar``.


   Python Packaging Authority (PyPA)

      PyPA_ is a working group that maintains many of
      the relevant projects in Python packaging.

   Python Package Index (PyPI)

      PyPI_ is the default :term:`Package Index` for the Python community.
      It is open to all Python developers to consume and distribute
      their distributions.

   Release

      A snapshot of a :term:`Project` at a particular point in time,
      denoted by a version identifier.

      Making a release may entail the publishing of multiple
      :term:`Distributions <Distribution Package>`.  For example, if version
      1.0 of a project was released, it could be available in both a source
      distribution format and a Windows installer distribution format.

   Requirement

      A specification for a :term:`package <Distribution Package>` to be
      installed.  pip_, the :term:`PyPA <Python Packaging Authority (PyPA)>`
      recommended installer, allows various forms of specification
      that can all be considered a *requirement*.

   Source Distribution (or *sdist*)

      A :term:`distribution <Distribution Package>` format (usually generated
      using ``python setup.py sdist``) that provides metadata and the
      essential source files needed for installing by a tool like pip_,
      or for generating a :term:`Built Distribution`.

   Version Specifier

      The version component of a requirement specifier.  For example,
      the ``>=1.3`` portion of ``foo>=1.3``.  :pep:`440` contains
      a :pep:`full specification <440#version-specifiers>`
      of the specifiers that Python packaging currently supports.

   Wheel

      A :term:`Built Distribution` format introduced by :pep:`427`.

.. _PyPA: https://pypa.io
.. _PyPI: https://pypi.org
.. _pip: https://pip.pypa.io
.. _IPFS: https://ipfs.io
