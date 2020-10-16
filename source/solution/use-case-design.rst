Use-Case Design
===============

Use-Case Realization
--------------------

Register
^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""
.. uml::

   actor Contributor
   boundary "Registration Form" as RF
   participant IVerification as V
   control "Registration Controller" as RC
   participant AccountDBManager as D
   entity AccountData

   activate Contributor
   Contributor -> RF : access()
   RF -> RF : prompt registration field()
   Contributor -> RF : register(input)
   RF -> V : request input verification()
   V -> RF : send error (AccountFormError)
   RF -> RF: display error()
   RF -> RF : prompt registration field()
   Contributor -> RF: register(input)
   RF -> V : request input verification()
   RC -> D: request account verification(username) 
   D -> AccountData : verify input()
   D -> RF: send error(DatabaseError)
   RF -> RF: display error()
   RF -> RF : prompt registration field()
   Contributor -> RF: cancel()

View of Participating Classes
"""""""""""""""""""""""""""""

..uml::

class "Registration Form" as RF extends Verification{
  UsernameField
  PasswordField
  EmailField
  getUsername()
  getPassword()
  getEmail()
  createAccount(username,password,email)
  displayError(error)
  requestform()
}
class Account{
 Username
 Password
 Email
 getUsername
 getPassword
 getEmail
}
RF -> Account
class IVerification<<interface>> {
 ValidName(Account.getName)
 ValidPassword(Account.getPassword)
 ValidEmail(Account.getEmail)
 VerifyQuery()

}
class Verification<<subsystem proxy>> extends IVerification
{
 ValidName(Account.getUsername)
 ValidPassword(Account.getPassword)
 ValidEmail(Account.getEmail)
 VerifyQuery(Account)
}
class "Registration Controller" as RC extends AccountDBManager

class AccountDBManager{
    getConnection()
    createQuery()
    search(Account)
    verify(result)
}
RF "0..1" -> "0..1" RC

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

Update
^^^^^^

Packages and Their Dependencies
-------------------------------
	