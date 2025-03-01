---
title: Enterprise High Availability Mode 2.x
layout: en_enterprise

---

## Travis CI Enterprise 2.x

Travis CI Enterprise 2.x typically runs as a single container instance communicating with one or multiple workers. Still, we also offer a High Availability configuration so you can run your installation with redundancy. High Availability Mode is a helpful way to have additional stability, particularly for customers with large-volume licenses.

If you're interested, or might be interested, in running Travis CI Enterprise in High Availability mode, please email us at [enterprise@travis-ci.com](mailto:enterprise@travis-cicom?subject:HA%20Mode), and we can discuss options and help you get started.

### Installation Overview

The platform installation is similar to the standard [Enterprise installation](/user/enterprise/setting-up-travis-ci-enterprise/#1-setting-up-enterprise-platform-virtual-machine), and the [worker installation](#installing-the-worker-in-high-availability-mode) is identical. However, there are some additional [system prerequisites](/user/enterprise/high-availability/), which means that to install in HA mode, you will need the following:
 * 3+ **16 gigs of RAM, 8 CPUs, 40GB HDD**, i.e. `c4.2xlarge` with a 40GB HDD. - 2+ for the VMs running the Platform and 1+ for the VMs running the Worker
 * [Redis](https://redis.io/), [RabbitMQ](https://www.rabbitmq.com/),
and [Postgres](https://www.postgresql.org/) instances
 * [GitHub OAuth app](/user/enterprise/setting-up-travis-ci-enterprise/#prerequisites), [trial license](/user/enterprise/setting-up-travis-ci-enterprise/#prerequisites) -- enabled for HA
 * Internet connection -- note, this installation is _not_ airgapped by default. Let [us know](mailto:enterprise@travis-ci.com) if you are interested in one.

### Install the Platform in High Availability Mode

HA is configured entirely on the Enterprise platform instance, but installing an HA platform is quite similar to installing a standard platform. The steps for HA are as follows.

1. Contact [enterprise@travis-ci.com](mailto:enterprise@travis-ci.com?subject=HA%20Installation) to have your Enterprise license configured for HA mode.
1. Set up your [platform instance using the standard installation steps](/user/enterprise/setting-up-travis-ci-enterprise/#1-setting-up-enterprise-platform-virtual-machine)
1. Sign in to your Admin Dashboard (at `https://<your-travis-ci-enterprise-domain>:8800`)
   1. Go to 'Settings' and click 'Enable HA'.
   1. Paste in the URLs where you have [Postgres](https://www.postgresql.org/), [Redis](https://redis.io/), and [RabbitMQ](https://www.rabbitmq.com/) hosted. The connection strings should be in the format of:
   ```
   postgres://user:password@url:port
   redis://user:password@url:port
   amqps://user:password@url:port
   ```
   1. Optional: Upload a RabbitMQ Client Certificate (`.crt`). This allows RabbitMQ to use TLS.
   1. Scroll down to the bottom of the page.
   1. Click 'Save' and restart.

Once your first platform instance is fully configured, you should be able to see the UI and request a build - your build will only run correctly if a worker is installed. Try out your new platform, and [please let us know](mailto:enterprise@travis-ci.com?subject=HA%20Troubleshooting) if you have questions.

#### Add more Platform Installations

We recommend at least two Platform containers for HA mode, and you can install more Enterprise containers in the same way you [installed](/user/enterprise/setting-up-travis-ci-enterprise/#1-setting-up-enterprise-platform-virtual-machine) the first.

Once your second platform is installed, its HA settings must also be configured. Go to the Admin Dashboard for your new platform container at `https://<your-second-travis-ci-enterprise-domain>:8800` to configure these as you did for [the first platform installation](#installing-the-platform-in-high-availability-mode).

## Install the Worker in High Availability Mode (all versions)

The worker installation works the same as non-HA installations, as do the build environment compatibility defaults per the Enterprise version. Check out the docs for which version of Enterprise handles different OS's([TCIE 2.x](/user/enterprise/setting-up-travis-ci-enterprise/#2-setting-up-the-enterprise-worker-virtual-machine) or [TCIE 3.x](/user/enterprise/tcie-3.x-setting-up-travis-ci-enterprise/#2-setting-up-the-enterprise-worker-virtual-machine) and other information regarding the installation. You must retrieve your RabbitMQ password from your installation rather than the Travis CI Enterprise Admin Dashboard.


## Contact Enterprise Support

{{ site.data.snippets.contact_enterprise_support }}
