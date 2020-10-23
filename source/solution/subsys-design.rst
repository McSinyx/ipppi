Subsystem Design
================

MetadataSystem
--------------

MetadataSystem::check against conflicts

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   participant MetadataSystemClient
   participant MetadataSystem

   activate MetadataSystemClient
   MetadataSystemClient -> MetadataSystem : check against conflicts(proposal)
   MetadataSystem -> PackageAnalyzer : analyze(packages)
   PackageAnalyzer -> PackageFetcher : fetch(packages)
   deactivate PackageAnalyzer
   deactivate PackageFetcher
   MetadataSystem -> IRDBConnector : get all package versions()
   deactivate IRDBConnector
   MetadataSystem -> IRDBConnector : get all package requirements()
   deactivate IRDBConnector
   MetadataSystem -> ConflictChecker : check(versions, requirements)
   deactivate ConflictChecker
   deactivate MetadataSystem

RDBConnector
------------

For connector to a ralational database, we use third-party library conforming
DB API v2.0 (:pep:`249`).
