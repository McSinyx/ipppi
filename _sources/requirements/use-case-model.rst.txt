Use-Case Model
==============

.. uml::

   skinparam defaultFontColor #a80036
   left to right direction

   actor "End-User" as User
   actor Contributor
   actor Maintainer
   actor "Distributed File System" as IPFS

   usecase "Download Packages" as Download
   usecase "Query Packages" as Query

   usecase Register
   usecase Login
   usecase "Change Status" as Change

   usecase "Propose Package Update" as Propose
   usecase "Check against Conflicts" as Check
   usecase "Review Proposal" as Review
   usecase "Update Packages" as Update

   User --> Query
   User --> Download
   Download --> IPFS

   Contributor --> Register
   Contributor --> Login

   Contributor --> Propose
   Propose ..> Check : <<include>>

   Contributor --> Change
   Change -- Maintainer

   Maintainer --|> Contributor
   Maintainer --> Review

   Update ..> Review : <<extend>>
   Update ..> Check : <<include>>
   Update --> IPFS


Download Packages
-----------------

Brief Description
^^^^^^^^^^^^^^^^^

This use case allows an End-User to download per desired packages
from the distributed file system.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

1. The End-User request for a set of packages
2. The system process the request and redirect to the Distributed File System
3. The Distributed File System deliver the packages to the End-User

Alternative Flows
"""""""""""""""""

Package Unavailable
   In step 2, if a requested package is not found in the system's database,
   the system should response appropriately.

Package Not Pinned
   In step 2, if a requested package is in the database but takes
   an indefinite amount of time be found in the distributed file system,
   the system should send a timeout response to the End-User.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

The system must support download through the `simple project API`_.

Pre-Conditions
^^^^^^^^^^^^^^

None.

Post-Conditions
^^^^^^^^^^^^^^^

The system state is unchanged by this use case.

Extension Points
^^^^^^^^^^^^^^^^

None.


Query Packages
--------------

Brief Description
^^^^^^^^^^^^^^^^^

This use case allows an End-User to search and inspect packages
within the system's database.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

1. The End-User send a search query to the system.
2. The system convert the query to use it to look up packages in the database.
3. The system send the End-User the list of matching packages.
4. The End-User select a package to inspect.
5. The system responds with the metadata of the package.

Alternative Flows
"""""""""""""""""

Too Many Matches
   In step 3, if the number of matches exceeds a certain threshold,
   the system only send a fraction of the list at a time.
   In the following step, the End-User may choose to either get
   the next slice of matches or proceed to step 4 in the basic flow.

Zero Match
   In step 2, if no package in the database matches the provided pattern,
   the system responses appropriately and the use case ends.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

None.

Post-Conditions
^^^^^^^^^^^^^^^

The system state is unchanged by this use case.

Extension Points
^^^^^^^^^^^^^^^^

None.


Register
--------

Brief Description
^^^^^^^^^^^^^^^^^

This use case lets a Contributor create an account.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

The use case starts when a Contributor tries to login but does not have an account
and wishes to create a new one.

1. The Contributor chooses to create a new account.
2. The system prompts for authentication information.
3. The Contributor enters the requested information.
4. The system verifies information.
5. The system creates an account accordingly.

Alternative Flows
"""""""""""""""""

Registration Cancelled
   In step 3, if the Contributor chooses to cancel the registration instead,
   the use case ends.

Invalid Entered Information
   In step 4, if the information is invalid, the system reports error
   and goes back to step 2.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

None.

Post-Conditions
^^^^^^^^^^^^^^^

If registration was cancelled, the system state is unchanged by this use case.
Otherwise a new account is added to the authentication database.

Extension Points
^^^^^^^^^^^^^^^^

None.


Login
-----

Brief Description
^^^^^^^^^^^^^^^^^

This use case authenticates a Contributor to allow per
to access functions modifying the system's database.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

The use case starts when a Contributor wishes to login
to perform actions that requires authentication.

1. The system prompt for authentication information.
2. The Contributor enters per authentication information.
3. The system validates the entered authentication information.
4. The system temporary logs the Contributor in.

Alternative Flows
"""""""""""""""""

Invalid Authentication Information
   After step 3, if the authentication information is invalid,
   the system reports error.  The Contributor can choose to either
   cancel the operation or go back to step 1.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

To avoid `brute-force attacks`_,
there should be timeouts upon invalid authentication requests.

Pre-Conditions
^^^^^^^^^^^^^^

The Contributor must not be logged onto the system before this use case begins.

Post-Conditions
^^^^^^^^^^^^^^^

If login was cancelled, the system state is unchanged by this use case.
Otherwise the Contributor is now logged into the system.

Extension Points
^^^^^^^^^^^^^^^^

None.


Change Status
-------------

Brief Description
^^^^^^^^^^^^^^^^^

This use case democratically turns a Contributor into a Maintainer.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

1. A Contributor request a change of status.
2. The system notifies existing Maintainers about the request.
3. At least one Maintainer advocates for the self-promoted Contributor.
4. The system keeps the application pending for a period of time
   for potential objections.
5. The system promotes the Contributor to a Maintainer.

Alternative Flows
"""""""""""""""""

Objected Request
   In step 4, any objection from any Contributor will be notified
   to Maintainers.  If at the end of the pending period, all objections
   are not resolved/dismissed, the use case ends.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

Participating Contributors and Maintainers must be logged in.

Post-Conditions
^^^^^^^^^^^^^^^

If at the end of the pending period no objection remains, the account
of the self-promoted Contributor is changed into type Maintainer.

Extension Points
^^^^^^^^^^^^^^^^

None.


Propose Package Update
----------------------

Brief Description
^^^^^^^^^^^^^^^^^

The use case allows the Contributor to creat a proposal for update
one or many distribution packages.  This includes adding, removing
and upgrading/downgrading them as appropriate by the situation.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

This use case starts when the Contributor wishes to create
a *Package Update Proposal*.

1. The system requests that the Contributor specify
   the name of packages to be updated.
2. The Contributor selects the package names.
3. The system requests the Contributor
   to provide the :term:`release <Release>` to be pinned.
4. The Contributor choose the release for each package,
   or leave the field blank to remove the package from the index.
5. The system automatically :ref:`check for conflicts <check>`
   within the new set of distributions.
6. The system notifies the Maintainers to review the proposal.

Alternative Flows
"""""""""""""""""

Requested Information Unavailable
   If, after step 2, no package name is provided, the system will
   report an error.  The Contributor can choose to either cancel the operation
   or provide at least one package name.

Failed Checks
   In step 5, if the automated check fails, go back to step 3.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

The Contributor must be logged onto the system before this use case begin.

Post-Conditions
^^^^^^^^^^^^^^^

The system state is unchanged.

Extension Points
^^^^^^^^^^^^^^^^

None.


.. _check:

Check against Conflicts
-----------------------

Brief Description
^^^^^^^^^^^^^^^^^

This use case checks for the compatibility between the packages presuming
a proposal is accepted.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

This use case starts when a proposal is submitted by a Contributor
or approved by a Maintainer.

#. Check the requirements of each package
   if they do not conflict with each other.
#. Report the result accordingly.

Alternative Flows
"""""""""""""""""

None.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

None.

Post-Conditions
^^^^^^^^^^^^^^^

None.

Extension Points
^^^^^^^^^^^^^^^^

None.


Review Proposal
---------------

Brief Description
^^^^^^^^^^^^^^^^^

This use case describes how a Maintainer decides to approve
or dismiss proposals presuming it has them.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Use case starts when a proposal is uploaded.

1. The Maintainer checks for available proposals.
2. The Maintainer decides whether to dismiss or approve the proposal.
3. The System updates the database accordingly.

Alternative Flows
"""""""""""""""""

None.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

The Maintainer must be logged onto the system before this use case begins.

Post-Conditions
^^^^^^^^^^^^^^^

The proposal database is updated according to the Maintainer's review.

Extension Points
^^^^^^^^^^^^^^^^

If the Maintainer approves the proposal,
proceed into the :ref:`Update <update>` use case.


.. _update:

Update Packages
---------------

Brief Description
^^^^^^^^^^^^^^^^^

This use case update the database and the package index
based on an approved proposal.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

The use case starts when a Maintainer approves a proposal.

1. The system checks proposed package updates against conflicts.
2. The system updates packages metadata in the database accordingly.
3. The system updates distribution packages in the distributed file system.

Alternative Flows
"""""""""""""""""

Update Causes Conflicts
   In the first step of the basic flow, if the proposed update causes conflicts,
   the system aborts the operation and the use-case ends.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

The considered proposal is approved by at least one Maintainer.

Post-Conditions
^^^^^^^^^^^^^^^

If no conflict is found, the database and the distributed file system
must be updated accordingly.

Extension Points
^^^^^^^^^^^^^^^^

None.

.. _simple project API:
   https://warehouse.readthedocs.io/api-reference/legacy.html#simple-project-api
.. _brute-force attacks: https://en.wikipedia.org/wiki/Brute-force_attack
