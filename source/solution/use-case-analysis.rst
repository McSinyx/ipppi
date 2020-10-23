Use-Case Analysis
=================

Register
--------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary "Registration Form" as RF
   control "Registration Controller" as RC
   entity AccountData

   activate Contributor
   Contributor -> RF : request register()
   RF -> RF : prompt registration field()
   deactivate RF
   deactivate RF

   Contributor -> RF : register(input)
   RF -> RC : request input verification()
   RC -> AccountData : verify input()
   AccountData --> RC : return verification result()

   RC -> AccountData : add new account()
   deactivate AccountData
   deactivate RC
   deactivate RF
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class RegistrationForm <<boundary>> {
      // request register()
      // prompt registration field()
      // register(input)
   }

   class RegistrationController <<control>> {
      // request input verification()
      // return verification result()
   }

   class AccountData <<entity>> {
      // verify input()
      // add new account()
   }

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" AccountData

Login
-----

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary LoginForm
   control LoginController
   entity AccountData

   activate Contributor
   Contributor -> LoginForm: start logging in()
   LoginForm -> LoginForm: prompt for authentication information()
   deactivate LoginForm
   deactivate LoginForm

   Contributor -> LoginForm: enter(authentication information)
   LoginForm -> LoginController: log in(authentication information)
   LoginController -> AccountData: verify(authentication information)
   deactivate AccountData
   deactivate LoginController
   deactivate LoginForm
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class LoginForm <<boundary>> {
      start logging in()
      prompt for authentication information()
      enter(authentication information)
   }

   class LoginController <<control>> {
      log in(authentication information)
   }

   class AccountData <<entity>> {
      verify(authentication information)
   }

   LoginForm "0..*" -- "1" LoginController
   LoginController "1" -- "1" AccountData

Propose Package Update
----------------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary ProposalForm
   control ProposalController
   entity MetadataSystem
   entity NotificationSystem

   activate Contributor
   Contributor -> ProposalForm : create package update proposal()
   ProposalForm -> ProposalForm : prompt for package names()
   ProposalForm -> ProposalForm : prompt for update(package)
   ProposalForm -> ProposalController : add proposal(updates)
   ProposalController -> MetadataSystem : check for conflicts(updates)
   ProposalController -> NotificationSystem : notify maintainers for reviews(updates)
   deactivate NotificationSystem
   deactivate MetadataSystem
   deactivate ProposalController
   deactivate ProposalForm
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class ProposalForm <<boundary>> {
      // create package update proposal()
      // prompt for package names()
      // prompt for update(package)
   }

   class ProposalController <<control>> {
      // add proposal(updates)
   }

   class MetadataSystem <<entity>> {
      // check for conflicts(updates)
   }

   class NotificationSystem <<entity>> {
      // notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalController
   ProposalController "1" -- "1" MetadataSystem
   ProposalController "1" -- "1" NotificationSystem

Review Proposal
---------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Maintainer
   boundary ReviewForm
   control UpdateControl
   entity Proposal

   activate Maintainer
   Maintainer -> ReviewForm : check proposal ()
   ReviewForm -> UpdateControl : request proposal ()
   UpdateControl -> Proposal : get proposal ()
   deactivate UpdateControl
   deactivate Proposal
   ReviewForm -> ReviewForm : display proposal ()
   deactivate ReviewForm
   deactivate ReviewForm
   Maintainer -> ReviewForm : approve proposal ()
   ReviewForm -> UpdateControl :approve proposal ()
   UpdateControl -> Proposal : change status to approved ()
   deactivate ReviewForm
   deactivate ReviewForm
   deactivate UpdateControl
   deactivate Maintainer
   deactivate ReviewForm
   deactivate Proposal

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class ReviewForm <<boundary>> {
      // check proposal ()
      // display proposal ()
      // approve proposal ()
   }

   class UpdateControl <<control>> {
      // get proposal ()
      // change status to approved ()
   }

   class Proposal <<entity>> {
      // change status()
      // get proposal()
   }

   ReviewForm "0..*" -- "1" UpdateControl
   UpdateControl "1" -- "1" Proposal

Update
------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   control UpdateControl
   entity MetadataSystem
   boundary DFSConnector
   actor DistributedFileSystem

   activate UpdateControl
   UpdateControl -> MetadataSystem : check against conflict()
   UpdateControl -> DFSConnector : update package()
   DFSConnector -> MetadataSystem : update to Metadata()
   DFSConnector -> DistributedFileSystem : update to DFS()
   deactivate MetadataSystem
   deactivate UpdateControl
   deactivate DistributedFileSystem

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class DFSConnector <<boundary>> {
      // update to DFS()
      // update to Metadata()
   }

   class UpdateControl <<control>> {
      // check against conflict()
      // update package()
   }

   class MetadataSystem <<entity>> {
      // store package()
   }

   UpdateControl "1" -- "1" DFSConnector
   UpdateControl "1" -- "1" MetadataSystem
Security
Analysis-Class-To-Analysis-Mechanism Map
----------------------------------------

+------------------------+---------------------------+
| Analysis Class         | Analysis Mechanism(s)     |
+========================+===========================+
| RegistrationForm       | None                      |
+------------------------+---------------------------+
| RegistrationController | Distribution              |
+------------------------+---------------------------+
| LoginForm              | None                      |
+------------------------+---------------------------+
| LoginController        | Distribution              |
+------------------------+---------------------------+
| AccountData            | Persistency, Security     |
+------------------------+---------------------------+
| ProposalForm           | Persistency               |
+------------------------+---------------------------+
| ProposalController     | Distribution              |
+------------------------+---------------------------+
| MetadataSystem         | Persistency               |
+------------------------+---------------------------+
| ReviewForm             | Persistency               |
+------------------------+---------------------------+
| UpdateController       | Distribution              |
+------------------------+---------------------------+
| Proposal               | Persistency               |
+------------------------+---------------------------+
| Distributed            | None                      |
+ File System            +                           +
| Interface              |                           |
+------------------------+---------------------------+
