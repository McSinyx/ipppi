Design Elements
===============

Subsystem Context Diagrams
--------------------------

MetadataSystem Subsystem
^^^^^^^^^^^^^^^^^^^^^^^^

Subsystem Interface Descriptions
""""""""""""""""""""""""""""""""

DFS Subsystem
^^^^^^^^^^^^^

Subsystem Interface Descriptions
""""""""""""""""""""""""""""""""

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
RegistrationController     Application::Authentication
LoginForm                  Middleware::Authentication
LoginController            Application::Authentication
AccountData                Business Services::Authentication
ProposalForm               Middleware::Update Proposal
ProposalController         Application::Update Proposal
MetadataSystem subsystem   Business Services
IMetadataSystem interface  Business Services::Package Index
ReviewForm                 Middleware::Update Proposal
UpdateController           Application::Update Proposal
Proposal                   Business Services::Update Proposal
DFS subsystem              Business Services
IDFS interface             Business Services::External System Interfaces
=========================  =============================================

Architectural Layers and Their Dependencies
-------------------------------------------

.. uml::

   package "<<layer>>\nApplication" as App
   package "<<layer>>\nBusiness\nServices" as BS
   package "<<layer>>\nMiddleware" as Mid
   package "Base Reuse" as Base

   App ..> BS
   BS ..> Mid
   Mid .[hidden].> Base

Layer Descriptions
^^^^^^^^^^^^^^^^^^

Application
   The Application layer contains application-specific design elements.

Business Services
   The Business Services layer contains business-specific elements
   that are used in several applications.

Middleware
   Utilities and platform-independent services.

Packages and Their Dependencies
-------------------------------
