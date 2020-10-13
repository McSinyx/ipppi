Design Elements
===============

Subsystem Context Diagrams
--------------------------

Verification Subsystem
^^^^^^^^^^^^^^^^^^^^^^

.. uml::

  class LoginController <<control>>
  
  class RegistrationController <<control>>
    
  class IVerification <<interface>>
  {
  verify(username,password)
  }
    
  class Verification <<subsystem proxy>> extends IVerification {
  verify(username,password)
  }
  
  class AccountData <<entity>>
    
  LoginController "0..1" --> "0..1" Verification
  RegistrationController "0..1" --> "0..1" Verification
  IVerification --> AccountData
  Verification --> AccountData

Subsystem Interface Descriptions:
"""""""""""""""""""""""""""""""""

IVerification: Encapsulates communications with external databases

verify: Sending a query to the database to check if the login/registration information is valid or not
