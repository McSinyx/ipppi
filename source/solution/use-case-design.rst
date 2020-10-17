Use-Case Design
===============

Use-Case Realization
--------------------

Register
^^^^^^^^

Login
^^^^^

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
   participant ISecurity as S
   control LoginController
   participant AccountDBManager as D
   entity AccountData
   entity Account

   Contributor -> LoginForm: start logging in()
   LoginForm -> LoginForm: prompt for authentication information()
   Contributor -> LoginForm: enter(authentication information)   
   LoginForm -> LoginForm: Check empty field()
   LoginForm -> S: Send data for encapsulate()
   S -> Account: Create()
   S -> D: Send account to verify()
   D -> AccountData: verify(authentication information)
   D -> LoginController: allowlogin(account)
   LoginController -> LoginForm: initate login(account) 

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036
   
   class Account <<entity>>{
     username
     password
     getUsername()
     getPassword()
   }
   class LoginForm <<boundary>> extends Security{
      usernamefield
      passwordfield
      start logging in()
      prompt for authentication information()
      enter(authentication information)
      isValid(usernamefield,passwordfield)
      send(authentication information)
   }
   class ISecurity <<interface>>{
      createAccount(username,password)
      send(Account)  
   }
   class Security<<subsystem proxy>> extends ISecurity{
      createAccount(username,password)
      send(Account)
   }
   class AccountDBManager{
      getConnection()
      createQuery()
      search(Account.username,Account.password)
      send(database information)
   }
   class LoginController <<control>> extends AccountDBManager {
       initiate login(database information)
   }
   
   class AccountData <<entity>> {
    
   }

   LoginForm "0..*" -- "1" LoginController
   LoginController "1" -- "1" AccountData
    Security -> Account
    Security "1" -- "1" AccountDBManager



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
