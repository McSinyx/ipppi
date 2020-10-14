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
RegistrationForm           Application::Authentication UI
RegistrationController     Application::Authentication Management
LoginForm                  Application::Authentication UI
LoginController            Application::Authentication Management
AccountData                Business Services::Authentication
ProposalForm               Application::Proposal Management
ProposalController         Application::Proposal Management
MetadataSystem subsystem   Business Services
IMetadataSystem interface  Business Services::Package Index
ReviewForm                 Application::Proposal Management
UpdateController           Application::Proposal Management
Proposal                   Business Services::Proposal Management
DFS subsystem              Middleware
IDFS interface             Middleware::External System Interfaces
=========================  =============================================

Architectural Layers and Their Dependencies
-------------------------------------------

.. uml::

   skinparam defaultFontColor #a80036

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

Authentication Management (from Application)

Authentication (from Business Services)

Proposal UI (from Application)

Proposal Management (from Business Services)

Package Index (from Business Services)

External System Interfaces (from Middleware)
