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

This use case started with the user sending his/her request to download his/her desired package, presumbably after Query use case for searching from the distributed file system.

1. The system requires that the request fulfilling all both criterias

*  The package
  
*  The package's version

2. Once the request is successfully sent from the user to the IPFS,it will send the file to the user


Alternative Flows
"""""""""""""""""

**Full Storage Warning**

* Before the download,if the remaining disk storage is not enough for the package downloaded,a warning would be sent. The user has the choice to go ahead or abort the download.

**Internet Connection Broken**

* If the user's internet connection is broken during the download,the system will display an error message.The user will have the option to either retry or abort.

**Full Storage Error**

* User's disk storage is full:If the user's internet connection is broken during the download,the system will display an error message.The user can either choose to retry or abort.

Special Requirements
^^^^^^^^^^^^^^^^^^^^
None

Pre-Conditions
^^^^^^^^^^^^^^

The user having the internet connection before and during the use case


Post-Conditions
^^^^^^^^^^^^^^^

The file is successfully downloaded

Extension Points
^^^^^^^^^^^^^^^^

Query
-----

Brief Description
^^^^^^^^^^^^^^^^^

This use case allows the user to search for the package in the database of files in IPFS, possibly for the Download Use Case.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

This use case starts with the user sending a query for his/her desired files in the database. 

1. A list of search results that are significantly simillar to the input of the user (either matching name,description or dependencies' name) will appear.

2. The user clicks into a result

3. A page of the result's package's information appears,showing its name,id,version,description,its shorterned name and a list of its dependencies


Alternative Flows
"""""""""""""""""

**Changing pages**

* There will be a limit of results in a page,so the user may have to go to other pages for his/her files.The user goes to another page of the query results.

**Direct Search**

* If the query result is 100% simillar to the package name in the database plus the version number, the user will be directed directly to the package's page
Special Requirements

**Dissimilar inputs**

* If the input is too dissimilar from the name of any input from the package, an error dialog will appear,asking the user to input better


Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

The user has internet connection


Post-Conditions
^^^^^^^^^^^^^^^

The user finds the information of his/her desired package

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
This use case checks for the compatibility between the packages presuming the proposal is accepted.

Actor: Contributor

Flow of Events
^^^^^^^^^^^^^^
This use case starts when distribution packages are submitted by contributors.

Basic Flow
""""""""""
1. Packages being updated(file addition/upgrade/removal).
2. Proposals are reviewed and automatically checked.
3. System provides solutions(modifications) to make sure that new updates do not cause conflicts within the package index.
4. Use case ends.

Actor: Maintainer 

Alternative Flows
"""""""""""""""""
* The proposal is not accepted *
1. System warnings.
2. System detects a functioning set of installs,or at least an install set that satisfies all projects' stated requirements.
2. System provides the latest compatible version of the packages.  

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^
Packages are downloaded.

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Review Proposal
---------------

Brief Description
^^^^^^^^^^^^^^^^^
This use case describes how a system decides to approve or dismiss proposals presuming it has them.
Actor: Maintainer
Actor: Contributor

Flow of Events
^^^^^^^^^^^^^^
Use case starts when a proposal is uploaded.

Basic Flow
"""""""""".
1. Contributor/Maintainer uploads proposals.
2. System checks the proposals.
3. System approves/dismisses proposals.

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^
The contributor/maintainer has internet connection.

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^
