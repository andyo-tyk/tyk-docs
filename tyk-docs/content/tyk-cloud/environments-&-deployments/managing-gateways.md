---
title: "Managing Edge Gateways"
date: 2020-08-21T14:58:21+01:00
tags: ["Tyk Cloud", "Management"]
description: "How to manage your Tyk Cloud Edge Gateways"
menu:
  main:
    parent: "Environments & Deployments"
weight: 4
aliases:
  - /tyk-cloud/environments-&-deployments/managing-gateways
---

## Introduction

Edge Gateways do all the heavy lifting of actually managing your requests: traffic proxying, access control, data transformation, logging and more.


## Prerequisites

All [user roles]({{< ref "tyk-cloud/teams-&-users/user-roles" >}}) can edit, deploy, undeploy, restart, redeploy all deployments within a team. Only the Organisation Admin and the Team Admin can create or delete deployments.


## Adding a new Edge Gateway

Watch our video on setting up a Control Plane and an Edge Gateway.

{{< youtube JqXXEDplrr8 >}}

{{< note success >}}
**Note**
  
The number of Edge Gateways you can add is dependent on your [plan]({{< ref "tyk-cloud/account-billing/plans" >}})
{{< /note >}}

1. From the Deployments screen click **Add Deployment**
2. Enter a name for the new Gateway
3. Select Edge Gateway from the Type drop-down list
4. Select the Bundle Channel and Version
5. (Optional) Enter a [custom domain]({{< ref "tyk-cloud/using-custom-domains" >}}) if required
6. (Optional) Enable [plugins]({{< ref "tyk-cloud/using-plugins" >}}) if required

## Edit Edge Gateways

You can edit the following Control Plane settings:
* Change the Gateway name
* Add a [custom domain]({{< ref "tyk-cloud/using-custom-domains" >}})
* Change the Bundle Channel and Bundle Version
* Enable [plugins]({{< ref "tyk-cloud/using-plugins" >}})

{{< note success >}}
**Note**
  
The use of custom domains is dependent on your [plan]({{< ref "tyk-cloud/account-billing/plans" >}})
{{< /note >}}

To edit an existing Edge Gateway:

1. On the Deployments screen, expand the Control Plane and click on the Edge Gateway to access the Edge Gateway overview screen.
2. Select **Edit** from the Deployed drop-down list

{{< img src="/img/admin/cp-edit.png" alt="Edge drop-down" >}}


## Upgrade Edge Gateways

To upgrade an existing Edge Gateway:

1. Go to the **Edge Gateway settings** using the _Edit Edge Gateways_ instructions and scroll down to the **Version** section.
2. Select a **Bundle Channel**.

{{< img src="/img/admin/cp-edge-upgrade-channel.png" alt="Bundle channel drop-down" >}}

3. Next, select a **Bundle Version**.

{{< img src="/img/admin/cp-edge-upgrade-version.png" alt="Bundle version drop-down" >}}

4. To apply your changes, click the **"Save and Re-Deploy"** button located at the top right. After a few seconds, you will be redirected to the overview page of the Control Plane and a **"Deploying"** indicator button will appear. 

{{< img src="/img/admin/cp-edge-upgrade-deploying.png" alt="Deploying notification" >}}

5. A **"Deployed"** button indicates a successful upgrade.

{{< img src="/img/admin/cp-edge-upgrade-deployed.png" alt="Deployed notification" >}}