# Deploying Apache Guacamole on Azure

In this post I'll show you how to create your own jump server using [Apache Guacamole](https://guacamole.apache.org/), an open source tool wich provide similar funcionalities from [Azure Bastion](https://docs.microsoft.com/en-us/azure/bastion/bastion-overview).

## Aapche Guacamole

Apache Guacamole is a clientless remote desktop gateway that supports standard protocols like VNC, RDP, and SSH. Clientless means your clients don't need to install anything but just use a web browser to remotely access your fleet of VMs.

The Guacamole comprises of two main components:

* Guacamole Server which provides guacd which is like a proxy server for the client to connect to the remote server.
* Guacamole Client which is a servelet container that user will log in and via web browser.

![guacamole-architecture.png](guacamole-architecture.png)
For more information about Guacamole, visit its [architecture page](https://guacamole.apache.org/doc/gug/guacamole-architecture.html).

## Guacamole on Azure Architecture

The drawing below refers to the suggested architecture. This architecture includes a public load balancer that receives external accesses and directs them to two virtual machines in the web layer. The web layer communicates with the data layer where we have a MySQL database responsible for storing login information, accesses and connections.

![azure-architecture.png](azure-architecture.png)

The Availability Set guarantees a 99.95% SLA for virtual machines and using Azure Database for MySQL, a highly available, scalable, managed database as a service guarantees a 99.99% SLA.

# Prerequisites

* Use the Bash environment in [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart).

[![launch-cloud-shell.png)](launch-cloud-shell.png)](http://shell.azure.com/)

* If you prefer, [install](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) the Azure CLI to run CLI reference commands.

* This tutorial requires version 2.0.4 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.
