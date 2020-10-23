Use-Case Design
===============

Use-Case Realization
--------------------

Register
^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor
   participant "Registration Form" as RF
   participant "Registration Controller" as RC
   participant AccountData

   activate Contributor
   Contributor -> RF : request register()
   RF -> RF : prompt registration field()
   deactivate RF
   deactivate RF

   Contributor -> RF : register(input)
   RF -> RC : request input verification()
   RC -> AccountData : verify input()
   deactivate AccountData
   RC -> AccountData : add new account()
   deactivate AccountData
   deactivate RC
   deactivate RF
   deactivate Contributor

Basic Flow (with Security)
''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor
   participant "Registration Form" as RF
   participant "Registration Controller" as RC
   participant AccountData
   participant ISecureUser <<interface>>

   activate Contributor
   Contributor -> RF : request register()
   RF -> RF : prompt registration field()
   deactivate RF
   deactivate RF
   Contributor -> RF : enter username()
   deactivate RF
   Contributor -> RF : enter password()
   deactivate RF
   Contributor -> RF : register account()
   RF -> RC : request input verification()
   RC -> AccountData : verify input()
   deactivate AccountData
   RC -> AccountData : add new account()
   deactivate AccountData   
   RC -> RC : setup security context()
   RC -> ISecureUser : new(UserID)
   deactivate ISecureUser
   deactivate RC
   deactivate RC   
   deactivate RF
   deactivate Contributor

View of Participating Classes
"""""""""""""""""""""""""""""

Register
''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class RegistrationForm {
      request register()
      prompt registration field()
      register(input)
   }

   class RegistrationController {
      request input verification()
   }

   class AccountData {
      verify input()
      add new account()
   }

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" AccountData

Register (with Security)
''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class RegistrationForm {
      request register()
      prompt registration field()
      enter username()
      enter password()
      register account()
   }

   class RegistrationController {
      request input verification()
      setup security context()
   }

   class AccountData {
      verify input()
      add new account()
   }
   
   interface ISecureUser <<interface>> {
      new()
   }   

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" AccountData
   RegistrationController "1" -- "1" ISecureUser

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

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor

   activate Contributor
   Contributor -> ProposalForm : create package update proposal()
   ProposalForm -> ProposalForm : prompt for package names()
   deactivate ProposalForm
   ProposalForm -> ProposalForm : prompt for update(package)
   ProposalForm -> ProposalCollection : add proposal(updates)
   ProposalCollection -> IMetadataSystem : check for conflicts(updates)
   ProposalCollection -> NotificationSystem : notify maintainers for reviews(updates)
   deactivate NotificationSystem
   deactivate IMetadataSystem
   deactivate ProposalCollection
   deactivate ProposalForm
   deactivate Contributor

Basic Flow (with Persistency)
'''''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor
   participant IRDBConnector <<interface>>

   activate Contributor
   Contributor -> ProposalForm : create package update proposal()
   ProposalForm -> ProposalForm : prompt for package names()
   deactivate ProposalForm
   ProposalForm -> ProposalForm : prompt for update(package)
   ProposalForm -> ProposalCollection : add proposal(updates)
   ProposalCollection -> IRDBConnector : insert_proposal(updates)
   ProposalCollection -> IMetadataSystem : check for conflicts(updates)
   ProposalCollection -> NotificationSystem : notify maintainers for reviews(updates)
   deactivate NotificationSystem
   deactivate IMetadataSystem
   deactivate ProposalCollection
   deactivate ProposalForm
   deactivate Contributor

View of Participating Classes
"""""""""""""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class ProposalForm {
      create package update proposal()
      prompt for package names()
      prompt for update(package)
   }

   class ProposalCollection {
      add proposal(updates)
   }

   interface IMetadataSystem <<interface>> {
      check for conflicts(updates)
   }

   class NotificationSystem {
      notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalCollection
   ProposalCollection "1" -- "1" IMetadataSystem
   ProposalCollection "1" -- "1" NotificationSystem

Basic Flow (with Persistency)
'''''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class ProposalForm {
      create package update proposal()
      prompt for package names()
      prompt for update(package)
   }

   class ProposalCollection {
      add proposal(updates)
   }

   interface IMetadataSystem <<interface>> {
      check for conflicts(updates)
   }

   interface IRDBConnector <<interface>> {
      insert_proposal(updates)
   }

   class NotificationSystem {
      notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalCollection
   ProposalCollection "1" -- "1" IRDBConnector
   ProposalCollection "1" -- "1" IMetadataSystem
   ProposalCollection "1" -- "1" NotificationSystem

Review Proposal
^^^^^^^^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Maintainer
   activate Maintainer
   Maintainer -> ReviewForm : check proposal ()
   ReviewForm -> UpdateControl : request proposal (uuid)
   UpdateControl -> ProposalCollection : get proposal (uuid)
   deactivate UpdateControl
   deactivate ProposalCollection
   ReviewForm -> ReviewForm : display proposal (uuid)
   deactivate ReviewForm
   deactivate ReviewForm
   Maintainer -> ReviewForm : approve proposal (uuid)
   ReviewForm -> UpdateControl : approve proposal (uuid)
   UpdateControl -> ProposalCollection : change status to approved (uuid)
   deactivate ProposalCollection
   deactivate UpdateControl
   deactivate ReviewForm
   deactivate Maintainer

Basic Flow (with Persistency)
'''''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Maintainer
   participant ReviewForm
   participant UpdateControl
   participant ProposalCollection
   participant IRDBConnector <<interface>>

   activate Maintainer
   Maintainer -> ReviewForm : check proposal ()
   ReviewForm -> UpdateControl : request proposal (uuid)
   UpdateControl -> ProposalCollection : get proposal (uuid)
   deactivate UpdateControl
   deactivate ProposalCollection
   ReviewForm -> ReviewForm : display proposal (uuid)
   deactivate ReviewForm
   deactivate ReviewForm
   Maintainer -> ReviewForm : approve proposal (uuid)
   ReviewForm -> UpdateControl : approve proposal (uuid)
   UpdateControl -> ProposalCollection : change status to approved (uuid)
   ProposalCollection -> IRDBConnector : change status to approved (uuid)
   deactivate ProposalCollection
   deactivate UpdateControl
   deactivate ReviewForm
   deactivate Maintainer

View of Participating Classes
"""""""""""""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class ReviewForm {
      check proposal (uuid)
      display proposal(uuid)
      approve proposal(uuid)
   }

   class UpdateControl {
      request proposal(uuid)
      approve proposal(uuid)
   }

   class ProposalCollection {
      get proposal(uuid)
      change status to approved(uuid)
   }

   ReviewForm "0..*" -- "1" UpdateControl
   UpdateControl "1" -- "1" ProposalCollection

Basic Flow (with Persistency)
'''''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class ReviewForm {
      check proposal (uuid)
      display proposal(uuid)
      approve proposal(uuid)
   }

   class UpdateControl {
      request proposal(uuid)
      approve proposal(uuid)
   }

   class ProposalCollection {
      get proposal(uuid)
      change status to approved(uuid)
   }

   interface IRDBConnector <<interface>> {
      change status to approved(uuid)
   }

   ReviewForm "0..*" -- "1" UpdateControl
   UpdateControl "1" -- "1" ProposalCollection
   IRDBConnector "1" -- "1" ProposalCollection

Update
^^^^^^

Packages and Their Dependencies
-------------------------------
