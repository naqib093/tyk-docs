---
date: 2017-03-15T15:01:42Z
title: Tyk Self-Managed
tags: ["Tyk Stack", "Self-Managed", "Installation"]
description: "What is the Tyk Self-Managed solution"
weight: 4
menu:
    main:
        parent: "API Management"
aliases:
  - /getting-started/installation/with-tyk-on-premises/
  - /tyk-on-premises/getting-started/
  - /getting-started/installation/with-tyk-on-premises/bootstrapper-cli/
  - /get-started/with-tyk-on-premise/
---
## What is Tyk On-Premises / Self-Managed ?

Tyk Self-Managed allows you to easily install our Full Lifecycle API Management solution in your own infrastructure. There is no calling home, and there are no usage limits.  You have full control.



## Tyk Components
The full Tyk Self-Managed system consists of:
<!-- todo: oss labels: -->
* [Tyk Gateway]({{< ref "tyk-oss-gateway" >}}):  Tyk Gateway is provided ‘Batteries-included’, with no feature lockout. It is an open source enterprise API Gateway, supporting REST, GraphQL, TCP and gRPC protocols, that protects, secures and processes your APIs.
* [Tyk Dashboard]({{< ref "tyk-dashboard" >}}): The management Dashboard and integration API manage a cluster of Tyk Gateways and also show analytics and features of the [Developer portal]({{< ref "tyk-developer-portal" >}}). The Dashboard also provides the API Developer Portal, a customisable developer portal for your API documentation, developer auto-enrollment and usage tracking.
* [Tyk Pump]({{< ref "tyk-pump" >}}): Tyk Pump handles moving analytics data between your gateways and your Dashboard (amongst other data sinks). The Tyk Pump is an open source analytics purger that moves the data generated by your Tyk nodes to any back-end.
* [Tyk Identity Broker]({{< ref "tyk-identity-broker" >}}) (Optional): Tyk Identify Broker handles integrations with third-party IDP's. It (TIB) is a component providing a bridge between various Identity Management Systems such as LDAP, Social OAuth (e.g. GPlus, Twitter, GitHub) or Basic Authentication providers, to your Tyk installation.
* [Tyk Multi-Data Center Bridge]({{< ref "tyk-multi-data-centre" >}}) (Optional, add-on): Tyk Multi-Data Center Bridge allows for the configuration of a Tyk ecosystem that spans many data centers and clouds. It also (MDCB) acts as a broker between Tyk Gateway Instances that are isolated from one another and typically have their own Redis DB.



## Architecture
{{< img src="/img/diagrams/diagram_docs_pump-data-flow@2x.png" alt="Tyk Self-Managed Archtecture" >}}

## Dependencies & Database Support

### MongoDB / PostgreSQL

Tyk Dashboard requires a persistent datastore for its operations. By default MongoDB is used. From Tyk v4.0, we also support PostgreSQL. See [Database Options]({{< ref "tyk-dashboard/database-options.md" >}}) for a list of versions and drop-in replacements we support.

### Redis

Tyk Gateway requires Redis for its operations. See [supported Redis versions]({{< ref "planning-for-production/redis#supported-versions">}}) for the list of releases.

Visit the [Gateway page]({{< ref "tyk-oss-gateway" >}}) for more info.


## Init Systems

Tyk packages support [systemd](https://www.freedesktop.org/wiki/Software/systemd/), [Upstart](http://upstart.ubuntu.com/cookbook/) (both 0.6.x and 1.x) and SysVinit Linux init systems. During package installation only one is chosen depending on the operating system support, e.g.:

*   CentOS 6, RHEL 6, Amazon Linux ship with Upstart 0.6.x
*   Ubuntu 14.04, Debian Jessie with Upstart 1.x
*   CentOS 7, RHEL 7, Ubuntu 16.04, Debian Stretch are running with systemd
*   Certain older distros may only provide SysVinit but all of them typically provide compatibility with its scripts

Note that any init scripts of your choosing can be used instead of automatically detected ones by copying them from the `install/inits` directory inside the package directory.

This init system variance implies there are different ways to manage the services and collect service logs.

#### Upstart
For Upstart, service management can be performed through the `initctl` or a set of `start`, `stop`, `restart` and `status` commands. Upstart 1.x also works with the `service` command.

#### systemd
For systemd, either `systemctl` or `service` commands may be utilized.

The `service` command can usually be used with SysVinit scripts, as well as invoking them directly.

## Service logs availability ##

*   Upstart 0.6.x and SysVinit: log files are located in `/var/logs` for every respective service, e.g. `/var/logs/tyk-gateway.stderr` and `/var/logs/tyk-gateway.stdout`
*   Upstart 1.x: by default everything is stored in `/var/logs/upstart` directory, e.g. `/var/logs/upstart/tyk-gateway.log`
*   systemd utilizes its own logging mechanism called journald, which is usable via the `journalctl` command, e.g. `journalctl -u tyk-gateway`


Please consult with respective init system documentation for more details on how to use and configure it.


## Free Trial

Sign up for a free trial to test it out:

{{< button_left href="https://tyk.io/sign-up#self" color="green" content="Try for free" >}}


## Installing Tyk Self-Managed
Please visit our [Self-Managed installation]({{< ref "tyk-self-managed/install" >}}) page to get started.


## Licensing

Read more about licensing [here]({{< ref "tyk-on-premises/licensing" >}}).
