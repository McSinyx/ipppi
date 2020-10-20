Use-Case Design
===============

Use-Case Realization
--------------------

Register
^^^^^^^^

Login
^^^^^

Interaction Diagrams
""""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor
   participant LoginForm
   participant Security as S
   participant LoginController
   participant AccountDBManager as D
   participant AccountData
   participant Account

   activate Contributor
   Contributor -> LoginForm: start logging in()
   LoginForm -> LoginForm: prompt for authentication information()
   deactivate LoginForm
   deactivate LoginForm
   Contributor -> LoginForm: enter(authentication information)   
   LoginForm -> LoginForm: check empty field()
   deactivate LoginForm
   LoginForm -> S: send data for encapsulate()
   deactivate LoginForm
   S -> Account: create()
   deactivate Account
   S -> D: send account to verify(account)
   deactivate S
   D -> AccountData: verify(account information)
   deactivate AccountData
   D -> LoginController: allowlogin(account)
   deactivate D
   LoginController -> LoginForm: initate login(account)
   deactivate LoginController
   deactivate LoginForm

View of Participating Classes
"""""""""""""""""""""""""""""

.. uml::

   skinparam defaultFontColor #a80036

   class Account {
     username
     password
     create()
   }

   class LoginForm extends Security {
      usernamefield
      passwordfield
      start logging in()
      prompt for authentication information()
      enter(authentication information)
      checkempty(usernamefield,passwordfield)
      initate login(account)
   }
   interface ISecurity <<interface>> {
      createAccount(username,password)
      send data for encapsulate()  
   }
   class Security <<subsystem proxy>> extends ISecurity {
      createAccount(username,password)
      send data for encapsulate()
   }
   class AccountDBManager {
      getConnection()
      send account to verify(account)
   }
   class LoginController extends AccountDBManager {
       allowlogin(account)
   }

   class AccountData {
       username
       password
       isMaintainer
       verify(account information)
   }

   LoginForm "0..*" -- "1" LoginController
   LoginController "1" -- "1" AccountData
   Security -> Account
   Security "1" -- "1" AccountDBManager
   AccountDBManager -> AccountData

Propose Package Update
^^^^^^^^^^^^^^^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor

   activate Contributor
   Contributor -> ProposalForm : create package update proposal()
   ProposalForm -> ProposalForm : prompt for package names()
   ProposalForm -> ProposalForm : prompt for update(package)
   ProposalForm -> ProposalController : add proposal(updates)
   ProposalController -> IMetadataSystem : check for conflicts(updates)
   ProposalController -> NotificationSystem : notify maintainers for reviews(updates)
   deactivate NotificationSystem
   deactivate IMetadataSystem
   deactivate ProposalController
   deactivate ProposalForm
   deactivate Contributor

View of Participating Classes
"""""""""""""""""""""""""""""

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

   interface IMetadataSystem <<interface>> {
      // check for conflicts(updates)
   }

   class NotificationSystem <<entity>> {
      // notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalController
   ProposalController "1" -- "1" IMetadataSystem
   ProposalController "1" -- "1" NotificationSystem

Review Proposal
^^^^^^^^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Maintainer
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
"""""""""""""""""""""""""""""

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
^^^^^^

Packages and Their Dependencies
-------------------------------
