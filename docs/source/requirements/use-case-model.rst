Use-Case Model
==============

.. uml::

   actor User
   actor Contributor
   actor Maintainer
   actor "Distributed File System" as IPFS

   usecase Download
   usecase Query

   usecase Register
   usecase Login
   usecase "Vote for New Maintainers" as Vote

   usecase "Propose Package Update" as Propose
   usecase "Check against Conflicts" as Check
   usecase "Review Proposal" as Review
   usecase Update

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

Download
--------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Query
-----

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

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
The maintainers of the database will vote for new maintainer when they need, replace, reduce maintainers

Flow of Events
Maintainers need more/less maintainer for the job, they will vote for new maintainer

Basic Flow
Maintainers need more/less maintainer for the job -> agree for human changes -> new maintainer login special account

Alternative Flows
alt 1. Maintainers need more/less maintainer for the job -> disagree for the new maintainers -> vote for another candidates
Special Requirements
^^^^^^^^^^^^^^^^^^^^
Maintainers:Need knowledges in project management

Pre-Conditions
^^^^^^^^^^^^^^
Lack of Human resources
Maintainers have low efficiently

Post-Conditions
^^^^^^^^^^^^^^^
New Candidates voted to become maintainers

Extension Points
^^^^^^^^^^^^^^^^

Propose Package Update
----------------------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Check against Conflicts
-----------------------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Review Proposal
---------------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Update
------

Brief Description
^^^^^^^^^^^^^^
This use case describes how an update operate.
Actor: Distributed File System 
Actor: Maintainer
Actor: Contributor

Flow of Events
^^^^^^^^^^^^^^ 
Use case start when a maintainer want to update package onto IFPS The maintainer review the packages proposed by the contributor The IFPS and maintainer will check for any conflict exist 
Basic Flow
"""""""""" 
The package will be checked against conflicts the contributor.
Next, the package will wait to be reviewed by the maintainer.
After that, the maintainer will decide to update the package to IFPS by schedule data, size, length, date of the update for the maintenance.After maintenance the maintainer will check for any conflicts, bugs maintain.

Alternative Flows
^^^^^^^^^^^^^^
Alt 1. The package will be checked against conflicts the contributor -> found conflicts -> the package is fixed by the contributor

alt 2. The package will wait to be reviewed by the maintainer -> the maintainer reject the package ->the package will not be updated -> the package is fixed by the contributor

alt 3. After maintenance, maintain any bug and conflicts -> the maintainer continue the maintenance -> the package will be fixed by the contributor and maintainer

Special Requirements
^^^^^^^^^^^^^^^^^^^^
Maintainers:
Contributor: have decent knowledges in HTML, SQL 

Pre-Conditions
^^^^^^^^^^^^^^
System need an update to increase performance
Bug, error founded

Post-Conditions
^^^^^^^^^^^^^^^
Minimal Guarantee: Bug, error reduced, maintenance update succesfully with no critical bug

Success Guarantee: BUg, error terminated, maintenance update succesfully

Extension Points
^^^^^^^^^^^^^^^^
