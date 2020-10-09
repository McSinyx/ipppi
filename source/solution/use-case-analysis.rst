Use-Case Analysis
=================

Register
----------------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::
   
   autonumber "#: //"
   hide footbox
   
   actor Contributor
   boundary "Registration Form" as RF
   control "Registration Controller" as RC
   entity Database

   activate Contributor
   Contributor -> RF : request register

   activate RF
   RF -> RF : prompt registration field
   activate RF
   Contributor -> RF : register(input)

   RF -> RC : request input verification
   activate RC
   RC -> Database : verify input
   activate Database
   Database --> RC : return verification result
   RC -> Database : add new account 
   deactivate Database
   deactivate RC

   deactivate RF
   deactivate RF
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   class RegistrationForm <<boundary>> {
      request register()
      prompt registration field()
      register(input)
   }

   class RegistrationController <<control>> {
      request input verification()      
      return verification result()
   }

   class Database <<entity>> {
      verify input()
      add new account()
   }

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" Database

Propose Package Update
----------------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary ProposalForm
   control ProposalController
   entity MetadataSystem
   boundary NotificationSystem

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

   class ProposalForm <<boundary>> {
      create package update proposal()
      prompt for package names()
      prompt for update(package)
   }

   class ProposalController <<control>> {
      add proposal(updates)
   }

   class MetadataSystem <<entity>> {
      check for conflicts(updates)
   }

   class NotificationSystem <<boundary>> {
      notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalController
   ProposalController "1" -- "1" MetadataSystem
   ProposalController "1" -- "1" NotificationSystem

Update
------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   autonumber "#: //"
   autoactivate on
   hide footbox

   actor System 
   boundary UpdatedPackage
   control UpdateControl    
   entity MetadataSystem

   activate System
   System -> UpdatedPackage :review proposal package()
   UpdatedPackage -> UpdateControl : update package()
   UpdateControl -> MetadataSystem : upload package()
   System -> System : reject proposal()
   System -> UpdatedPackage :review other proposal
   UpdatedPackage -> UpdateControl : update package()
   UpdateControl -> MetadataSystem : upload package()
   deactivate System
   deactivate MetadataSystem
   deactivate UpdateControl
   deactivate UpdatedPackage

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

 class UpdatedPackage <<boundary>> {
      //Display update()
      //GetPackageInfo()
      //Update()
   }

   class UpdateControl  <<control>> {
      //UploadPackage()
   }

   class MetadataSystem <<entity>> {
      //Store Update()
      //Display Update()
      //Update()
   }

   class System <<entity>> {
      //Review Package()
   }

   UpdatedPackage "0..*" -- "1" UpdateControl
   UpdateControl "1" -- "1" MetadataSystem
   UpdateControl "1" -- "0..*" System


