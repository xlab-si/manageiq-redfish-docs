Firmware updates functionality
==============================

The ManageIQ's Physical Infrastructure management has the ability to perform
firmware updates against the physical systems that support it. Specifically,
we have implemented this functionality in the Redfish Physical Infrastructure
provider.

Basic terms
-----------

A **firmware update** is an action of bringing some system's firmware to a
desired target firmware version.

A **firmware update binary** is a package containing an actual payload that
needs to be consumed in the process of updating the firmware by the target
physical system.

A **firmware update registry** is a service external to ManageIQ that contains
the list and the metadata to the available firmware update binaries.


Use cases
---------

This functionality addresses the following use cases:

* **Inventory of the available firmware update binaries**. The user registers
  a firmware update registry endpoint in their ManageIQ appliance and obtains
  a list of the available firmware update binaries.
* **Firmware update filtering**. The user selects between only the firmware
  update images that apply to a particular physical system's vendor and model.
* **Application of firmware updates**. The user requests a firmware update for
  the selected physical systems. The ManageIQ appliance executes the firmware
  update with the result of the target physical system being updated (or the
  firmware update failure).

Inventory of firmware update binaries
-------------------------------------

The list of registered firmware update registries and the list of firmware
update binaries is available in *Compute* > *Physical Infrastructure*. Here,
the user can use the *Configuration* > *Add a New Firmware Update Registry* to
register a registry's endpoint with the ManageIQ appliance. The ManageIQ will
populate the firmware update binaries lists automatically with the data from
the registry.

Requesting a firmware update
----------------------------

The user can request a firmware update by starting in a list of physical
infrastructure's list of physical servers. They can select one or more servers
from the list, or visit the details of a particular one server. Clicking on
*Lifecycle* > *Update Firmware* brings a dialog for selecting the firmware
update binary to apply. When the user confirms the chosen parameters, the
request for the firmware update is created.

Applying a firmware update
--------------------------

When a privileged user confirms the request, the ManageIQ invokes an internal
state machine that is implemented in the Redfish Physical Infrastructure
provider.
