Supplementary Specification
===========================

Objectives
----------

This section lists the requirements that are not readily captured
in the use-case model.  The supplementary specification together with
the use-case model capture a complete set of requirements on the system.

Scope
-----

This specification defines the non-functional requirements of the system
such as reliability, usability, performance, and supportability as well as
functional requirements that are common across a number of use cases.
(The functional requirements are defined in the Use Case Specifications.)

References
----------

:pep:`503`
   Simple Repository API

Functionality
-------------

None.

Usability
---------

The package index to be provided to end-users should behave analogous to PyPI
and support the `simple project API`_.  Package installers like ``pip``
should have no problem using an index provided by our project.

Reliability
-----------

The proposal and voting system must be available 99.99% of the time
(that is, there must be no more than a few seconds of outage a day).

The package index simply redirect to IPFS, and such service must have
the same availability.  The reliability of files hosted on IPFS is not within
the scope of this project, however it is improved as more are IPFS nodes
pin (mirror) them.

Performance
-----------

The provided package index should outperform PyPI when ``pip`` is invoked with
``--use-feature=2020-resolver``.  Ideally, package installers should have
an option to disable resolution backtracking to minimize execution time
on end-users' machine, but such issue if out of the scope of this project.

The proposal and voting system should be able to support up to 1000
contributors/maintainers simultaneously performing different tasks
at any given time.

Supportability
--------------

None.

Security
--------

The system must be able to prevent malicious entities from altering
the pinned releases.  In other words, the authencation system must ensure
only maintainers have write access to update the index.

Design Constraints
------------------

The system shall integrate with the distributed file system IPFS to serve
package distributions.

.. _simple project API:
   https://warehouse.readthedocs.io/api-reference/legacy.html#simple-project-api
