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
This use case allows the user to download his/her desired package from the distributed file system 

Flow of Events
^^^^^^^^^^^^^^
This use case started with the user sending his/her request to download his/her desired package,presumbably after Query use case for searching, from the distributed file system

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
* If the user's internet connection is broken during the download,the system will display an error message.The user can either choose to retry or abort.

Special Requirements
^^^^^^^^^^^^^^^^^^^^
None

Pre-Conditions
^^^^^^^^^^^^^^
The user has internet connection

Post-Conditions
^^^^^^^^^^^^^^^
The package is successfully downloaded

Extension Points
^^^^^^^^^^^^^^^^

Query
-----

Brief Description
^^^^^^^^^^^^^^^^^
This use case allows the user to search for the package in the database of files in IPFS,possibly for the Download Use Case.

Flow of Events
^^^^^^^^^^^^^^
This use case starts with the user sending a query for his/her desired files in the database. 

Basic Flow
""""""""""
1. A list of search results that are significantly simillar to the input of the user (either matching name,description or dependencies' name) will appear.
2. The user clicks into a result
3. A page of the result's package's information appears,showing its name,id,version,description,its shorterned name and a list of its dependencies

Alternative Flows
"""""""""""""""""
*There will be a limit of results in a page,so the user may have to go to other pages for his/her files.The user goes to another page of the query results.

*If the query result is 100% simillar to the package name in the database plus the version number, the user will be directed directly to the package's page
*If the input is too dissimilar from the name of any input from the package, an error dialog will appear,asking the user to input better


Special Requirements
^^^^^^^^^^^^^^^^^^^^
None

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
