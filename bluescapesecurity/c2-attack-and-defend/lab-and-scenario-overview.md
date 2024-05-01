# Lab and Scenario Overview

{% hint style="danger" %}
## Finish this Series First !

**DFIR Series Road Map:**

* [Getting Started](https://bluecapesecurity.com/getting-started/)
* [Build Your Forensic Workstation](https://bluecapesecurity.com/build-your-forensic-workstation/)
* [Prepare Your Target System(s)](https://bluecapesecurity.com/prepare-your-target-system/)
* [Attack & Defend Your Lab (mini-course)](https://bluecapesecurity.com/attack-and-defend-your-lab/)
* [Create Attack Scenarios](https://bluecapesecurity.com/training-scenarios/)
* [Perform Investigations and Analysis](https://bluecapesecurity.com/dfir-investigations/)
* [Build Your Lab ](https://bluecapesecurity.com/build-your-lab/)
  * [Virtualization Primer](https://bluecapesecurity.com/build-your-lab/virtualization/)
  * [Basic Lab](https://bluecapesecurity.com/build-your-lab/basic-lab/)
  * [Medium Lab](https://bluecapesecurity.com/build-your-lab/medium-lab/)
  * [Advanced Lab](https://bluecapesecurity.com/build-your-lab/advanced-lab/)
  * [Splunk Lab Installation](https://bluecapesecurity.com/build-your-lab/splunk-lab-installation/)
  * [Velociraptor Setup](https://bluecapesecurity.com/build-your-lab/velociraptor-setup/)
{% endhint %}

## Prerequisites

**Lab Setup**

* Create a lab that includes one or more Windows VMs. See [basic lab](https://bluecapesecurity.com/build-your-lab/basic-lab/) or [medium lab](https://bluecapesecurity.com/build-your-lab/medium-lab/) setup.
* [Prepare your target system.](https://bluecapesecurity.com/prepare-your-target-system/)
  * Disable Windows Defender and any security controls.
  * Install Sysinternals Sysmon.
* Add a [Kali Linux VM](https://www.kali.org/) to the lab environment.

**Tooling**

* [Install Splunk ](https://bluecapesecurity.com/build-your-lab/splunk-lab-installation/)and configure event log forwarding.
* [Install Velociraptor](https://bluecapesecurity.com/build-your-lab/velociraptor-setup/) server and clients.
* [Download forensic tools](https://bluecapesecurity.com/build-your-forensic-workstation/) such as Eric Zimmerman Tools and CyberChef.

**Pre-Attack Tests**

* Ensure that your host and client systems can communicate. Note the VM IP addresses.
* Ensure that you see event logs including Sysmon events in Splunk.
* Ensure that Windows VMs are online in Velociraptor.
* Ensure that the Kali Linux VM can connect to the Windows VM.
* Ensure that Windows VMs have Defender and security controls permanently turned off.
