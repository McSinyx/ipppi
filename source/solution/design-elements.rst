Design Elements
===============

Subsystem Context Diagrams
--------------------------

Verification Subsystem
^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class LoginController <<control>>

   class RegistrationController <<control>>

   class IVerification <<interface>> {
      verify(username, password)
   }

   class Verification <<subsystem proxy>> extends IVerification {
      verify(username, password)
   }

   class AccountData <<entity>>

   LoginController "0..1" --> "0..1" Verification
   RegistrationController "0..1" --> "0..1" Verification
   IVerification --> AccountData
   Verification --> AccountData

Subsystem Interface Descriptions
""""""""""""""""""""""""""""""""

``IVerification``: Encapsulates communications with external databases
   ``verify``: Sending a query to the database to check
   if the login/registration information is valid or not

Analysis-Class-to-Design-Element Map
------------------------------------

+------------------------+---------------------------+
| Analysis Class         | Design Element            |
+========================+===========================+
| RegistrationForm       | RegistrationForm          |
+------------------------+---------------------------+
| RegistrationController | RegistrationController    |
+------------------------+---------------------------+
| LoginForm              | LoginForm                 |
+------------------------+---------------------------+
| LoginController        | LoginController           |
+------------------------+---------------------------+
| AccountData            | AccountData               |
+------------------------+---------------------------+
| ProposalForm           | ProposalForm              |
+------------------------+---------------------------+
| ProposalController     | ProposalController        |
+------------------------+---------------------------+
|                        | MetadataSystem subsystem  |
+ MetadataSystem         +---------------------------+
|                        | IMetadataSystem interface |
+------------------------+---------------------------+
| ReviewForm             | ReviewForm                |
+------------------------+---------------------------+
| UpdateController       | UpdateController          |
+------------------------+---------------------------+
| Proposal               | Proposal                  |
+------------------------+---------------------------+
| Distributed            | DFS subsystem             |
+ File System            +---------------------------+
| Interface              | IDFS interface            |
+------------------------+---------------------------+

Design-Element-to-Owning-Package Map
------------------------------------

=========================  =============================================
Design Element             “Owning” Package
=========================  =============================================
RegistrationForm           Middleware::Authentication
RegistrationController     Applications::Authentication
LoginForm                  Middleware::Authentication
LoginController            Applications::Authentication
AccountData                Business Services::Authentication
ProposalForm               Middleware::Update Proposal
ProposalController         Applications::Update Proposal
MetadataSystem subsystem   Business Services
IMetadataSystem interface  Business Services::Package Index
ReviewForm                 Middleware::Update Proposal
UpdateController           Applications::Update Proposal
Proposal                   Business Services::Update Proposal
DFS subsystem              Business Services
IDFS interface             Business Services::External System Interfaces
=========================  =============================================
