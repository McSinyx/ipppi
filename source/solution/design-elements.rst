Design Elements
===============
LoginController
----------------------
Verification Subsystem
^^^^^^^^^^^^^^^^^^^^

.. uml::

  class LoginController<<control>>
    
  class IVerification<<interface>>
  {
  verify(username,password)
  }
    
  class Verification<<subsystem proxy>> extends IVerification {
  verify(username,password)
  }
    
  LoginController "0..1" - "0..1" Verification


Subsystem Interface Descriptions:
----------------------
IVerification:Encapsulates communications with external databases

verify:Sending a query to the database to check if the login information is valid or not
