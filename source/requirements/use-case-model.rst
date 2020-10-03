Use-Case Model
==============

.. uml::

   actor "End-User" as User
   actor Contributor
   actor Maintainer
   actor "Distributed File System" as IPFS

   usecase "Download Packages" as Download
   usecase "Query Packages" as Query

   usecase Register
   usecase Login
   usecase "Vote for New Maintainers" as Vote

   usecase "Propose Package Update" as Propose
   usecase "Check against Conflicts" as Check
   usecase "Review Proposal" as Review
   usecase "Update Packages" as Update

   User --> Query
   User --> Download
   Download --> IPFS

   Maintainer --> Vote
   Vote ..> Login : <<include>>

   Maintainer --|> Contributor
   Contributor --> Register

   Contributor --> Propose
   Propose ..> Login : <<include>>
   Propose ..> Check : <<include>>

   Maintainer --> Review
   Review ..> Login : <<include>>

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

This use case describes how a user creates an account.

Actor: New contributor/Contributor with no account (Guest)

Flow of Events
^^^^^^^^^^^^^^

The use case starts when a contributor visits the login page.
If perse doesn't have an account, perse can create a new one.

Basic Flow
""""""""""

1. The contributor select the registration option on the login page.
2. The System prompts contributor for registration information: Username, Password, etc
3. The contributor enters the information.
4. System verifies information and creates account.
5. The use case ends.

Alternative Flows
"""""""""""""""""

* **Cancel Registration**

  * The contributor select the cancel option.
  * The system returns the contributor to the login page, all information entered is deleted.

* **Invalid entered information**

  * Contributor finishes the registration form.
  * The system checks and shows the invalid information
  * Contributor re-enters the invalid information.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

No special requirements.

Pre-Conditions
^^^^^^^^^^^^^^

No pre-conditions.

Post-Conditions
^^^^^^^^^^^^^^^

* **Success**: The contributor now has had his/her own account and can use it to log in.
* **Failure**: The contributor is returned to the home page and continues to be a guest.

Extension Points
^^^^^^^^^^^^^^^^

No extension points.

Login
-----

Brief Description
^^^^^^^^^^^^^^^^^

This use case describes how a contributor logs into the system.

Actor: Contributor with created account 

Flow of Events
^^^^^^^^^^^^^^

The use case starts when a contributor is not logged in to the system and goes to the login page. 

Basic Flow
""""""""""

1. The contributor enters his/her username and password.
2. The system validates the entered username and password.
3. The contributor is signed in and returned to the home page as a Logged In Contributor.
4. The use case ends.

Alternative Flows
"""""""""""""""""

* **Wrong username/password**

  * The system shows why the contributor is not authenticated.
  * The contributor re-enters the information.
  * The Basic Flow continues after the contributor enters the information (From step 2).

Special Requirements
^^^^^^^^^^^^^^^^^^^^

No special requirements.

Pre-Conditions
^^^^^^^^^^^^^^

No pre-conditions.

Post-Conditions
^^^^^^^^^^^^^^^

* **Success**: The contributor is logged in and is able to to do specific actions.
* **Failure**: The contributor continues to be a guest.

Extension Points
^^^^^^^^^^^^^^^^

No extension points.

Vote for New Maintainers
------------------------

Brief Description
^^^^^^^^^^^^^^^^^

The maintainers of the database will vote for new maintainer
from existing contributors.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

#. Contributor/Maintainer nominate a Contributor as a new Maintainer.
#. System notify existing Maintainers for a vote.
#. Maintainers vote.
#. System update permission of Contributor to Maintainer if over 50% approved.

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

#. The system requests that the Contributor specify
   the name of packages to be updated.
#. Once the Contributor selects the package names, the system requests
   that the Contributor provide the :term:`release <Release>` to be pinned.
   The Contributor may leave the field blank to remove the package
   from the index.
#. The system notify the Maintainer to review the proposal,
   while at the same time automatically check for conflicts
   within the new set of distributions.
#. If the Maintainer request changes or the automated check fails,
   the previous step is repeated.

Alternative Flows
"""""""""""""""""

Requested Information Unavailable
   If, in the Basic Flow, no package name is provided, the system will
   display an error message.  The Contributor can choose to either
   cancel the operation or provide at least one package name.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

The Contributor must be logged onto the system before this use case begin.

Post-Conditions
^^^^^^^^^^^^^^^

Success: The new proposal is either dismissed or approved.

Failure: The system state is unchanged.

Extension Points
^^^^^^^^^^^^^^^^

None.

Check against Conflicts
-----------------------

Brief Description
^^^^^^^^^^^^^^^^^

This use case checks for the compatibility between the packages presuming
the proposal is accepted.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

This use case starts when distribution packages are submitted by contributors.

#. Check if the requirements of each package if they do not conflict
   with each other.
#. If there exists conflict, report failure, otherwise report success.

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

#. Maintainer checks for available proposals.
#. Maintainer decide whether to dismiss or approve the proposal.
#. System update the database accordingly.

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

If the Maintainer approve the proposal, proceed into the Update use case.

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
