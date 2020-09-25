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
| This use case describes how a user creates an account.
| Actor: Guest

Flow of Events
^^^^^^^^^^^^^^
| The use case starts when a system user visits the login page. 
| If he/she doesn't have an account, he/she can create a new one. 

Basic Flow
""""""""""
1. The user select the registration option on the login page.
2. The System prompts user for registration information: Username, Password, etc
3. The user enters the information.
4. System verifies information and creates account.
5. The use case ends.

Alternative Flows
"""""""""""""""""
* Cancel Registration   
   * The user select the cancel option.
   * The system returns the user to the login page, all information entered is deleted.

* Invalid entered information
   * User finishes the registration form.
   * The system checks and shows the invalid information
   * User re-enters the invalid information.

Special Requirements
^^^^^^^^^^^^^^^^^^^^
No special requirements.

Pre-Conditions
^^^^^^^^^^^^^^
No pre-conditions.

Post-Conditions
^^^^^^^^^^^^^^^
* Success: The user now has had his/her own account and can use it to log in.
* Failure: The user is returned to the home page and continues to be a guest.

Extension Points
^^^^^^^^^^^^^^^^
No extension points.

Login
-----

Brief Description
^^^^^^^^^^^^^^^^^
| This use case describes how a user logs into the system.
| Actor: User with created account 

Flow of Events
^^^^^^^^^^^^^^
The use case starts when a system user is not logged in to the system and goes to the login page. 

Basic Flow
""""""""""
1.	The user enters his/her username and password.
2.	The system validates the entered username and password.
3.	The user is signed in and returned to the home page as a Logged In User.
4.	The use case ends.

Alternative Flows
"""""""""""""""""
* Wrong username/password
   * The system shows why the user is not authenticated.
   * The user re-enters the information.
   * The Basic Flow continues after the user enters the information (From step 2).

Special Requirements
^^^^^^^^^^^^^^^^^^^^
No special requirements.

Pre-Conditions
^^^^^^^^^^^^^^
No pre-conditions.

Post-Conditions
^^^^^^^^^^^^^^^
* Success: The user is logged in and is able to to do specific actions.
* Failure: The user continues to be a guest.

Extension Points
^^^^^^^^^^^^^^^^
No extension points.

Vote for New Maintainers
------------------------

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
