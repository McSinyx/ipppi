Use-Case Design
===============

Use-Case Realization
--------------------

Register
^^^^^^^^

Login
^^^^^

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
