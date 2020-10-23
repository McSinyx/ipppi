Class Design
============

Register
^^^^^^^^
   
.. uml::
   
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

.. uml::
   
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

.. uml::
   
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

.. uml::
   
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
   
.. uml::
   
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
   
   interface DFSsubsystem <<interface>> {
      // display package()
   }   
   UpdateControl "1" -- "1" DFSConnector
   UpdateControl "1" -- "1" MetadataSystem
    
  
