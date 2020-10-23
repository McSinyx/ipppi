Run-time Architecture
=====================

Concurrency
-----------

* Multiple users can download the same package at the same time

* Users will be notified if the package they choose to download is being updated

* Multiple users can login/register at the same time

* Updates can be proposed even when the last package still being reviewed

Process Model
-------------

.. uml::

    rectangle userInterface <<thread>>
    rectangle downloadThread <<thread>>
    rectangle updateThread <<thread>>
    rectangle reviewThread <<thread>>
    rectangle checkconflict <<thread>>
    rectangle DFSconnector <<thread>>
    rectangle metadataThread <<thread>>
    rectangle querryThread <<thread>>
    rectangle ipppiController <<controller>>
    rectangle updateController <<controller>>
    rectangle proposalForm <<boundary>>
    rectangle updateForm <<boundary>>
    rectangle reviewForm <<boundary>>
    rectangle ipppiForm <<boundary>>
    rectangle metadatasubsystem <<subsystem proxy>>
    rectangle DFSsubsystem <<subsystem proxy>>

    userInterface "0..*" <--> "1" ipppiController
    checkconflict "0..*" <--> "1" ipppiController
    userInterface "0..*" <--> "0..*" downloadThread
    userInterface "0..*" <--> "0..*" reviewThread
    reviewThread "0..*" <--> "1" reviewForm
    userInterface "0..*" <--> "0..*" updateThread
    updateThread "0..*" <--> "1" updateForm
    DFSsubsystem "1" <--> "1" DFSconnector
    metadatasubsystem "1" <--> "0..*" metadataThread
    downloadThread "0..*" <--> "1" DFSconnector
    updateThread "0..*" <--> "0..*" metadataThread
    updateThread "0..*" <--> "1" updateController
    updateThread "0..*" <--> "1" DFSconnector
    userInterface "0..*" <--> "1" ipppiForm
    updateThread "0..*" <--> "0..*" querryThread
    updateThread "0..*" <--> "1" proposalForm
