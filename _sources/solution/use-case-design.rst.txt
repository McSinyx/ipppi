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

Iteraction Diagrams
"""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   participant UpdateControl
   participant IMetadataSystem <<interface>>
   participant DFSConnector
   actor DistributedFileSystem

   activate UpdateControl
   UpdateControl -> IMetadataSystem : check against conflict()
   deactivate IMetadataSystem
   UpdateControl -> IMetadataSystem : update metadata()
   deactivate IMetadataSystem
   UpdateControl -> DFSConnector : upload package()
   DFSConnector -> DistributedFileSystem : upload()
   deactivate IMetadataSystem
   deactivate UpdateControl
   deactivate DistributedFileSystem

View of Participating Classes
"""""""""""""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class UpdateControl

   class DFSConnector {
      upload package()
   }

   interface IMetadataSystem <<interface>> {
      check against conflict()
      update metadata()
   }

   UpdateControl "1" -- "1" DFSConnector
   UpdateControl "1" -- "1" IMetadataSystem

Packages and Their Dependencies
-------------------------------

.. uml::

   skinparam defaultFontColor #a80036

   package "Authentication UI\n(from Application)" as AuthUI
   package "Authentication Management\n(from Application)" as AuthMgm
   package "Authentication\n(from Business Services)" as Auth
   package "Proposal UI\n(from Application)" as ProposeUI
   package "Proposal Management\n(from Business Services)" as ProposeMgm
   package "Package Index\n(from Business Services)" as PI
   package "External System Interfaces\n(from Middleware)" as ExtI

   AuthUI --> AuthMgm
   AuthMgm --> Auth
   ProposeUI --> ProposeMgm
   ProposeMgm --> PI
   ProposeMgm --> ExtI


Package Descriptions
^^^^^^^^^^^^^^^^^^^^

Authentication UI (from Application)
   Interface for maintainers/contributors to initate login/register

Authentication Management (from Application)
   Allow or disallow login/register request 

Authentication (from Business Services)
   Containing account's information for manintainer/contributors to login/register

Proposal UI (from Application)
   Interface for contributor's proposal for packages
 
Proposal Management (from Business Services)
   Managing proposal from contributors for either accept or dismiss
   
Package Index (from Business Services)
   Handling package 
   
External System Interfaces (from Middleware)
   Interface for IDFS for downloading files
