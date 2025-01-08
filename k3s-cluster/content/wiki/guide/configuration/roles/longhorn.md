---
title: Longhorn
prev: /wiki/guide/configuration/roles
next: /wiki/guide/configuration/roles/prometheus
---

The role performs various tasks related to Helm chart deployment, reset and validation.

<!--more-->

## Role Settings

See the related role settings listed below, defined into [`main.yaml`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/defaults/main.yaml) defaults file.

{{% steps %}}

### `longhorn_vars.kubernetes`

- Default value: `null`

See the related child settings, listed below.

{{% steps nested="true" %}}

#### `kubernetes.default_settings`

- Default value: `null`

{{% steps %}}

##### `default_settings.backup`

- Default value: `null`

{{% steps %}}

###### `backup.enabled`

- Default value: `boolean`, `false`

###### `backup.secret`

- Default value: `null`

{{% steps %}}

###### `secret.name`

- Default value: `string`, `longhorn-secret`

{{% /steps %}}

###### `backup.target`

- Default value: `string`, `nfs://server:/mount`

###### `backup.user`

- Default value: `null`

{{% steps %}}

###### `user.name`

- Default value: `string`, `user`

###### `user.password`

- Default value: `string`, `password`

Encrypt the variable with [`ansible-vault`](/k3s-cluster/tutorials/handbook/ansible/#vault).

{{% /steps %}}

{{% /steps %}}

##### `default_settings.data_locality`

- Default value: `string`, `strict-local`

##### `default_settings.orphan_auto_deletion`

- Default value: `boolean`, `true`

##### `default_settings.pod_deletion_policy`

- Default value: `string`, `delete-both-statefulset-and-deployment-pod`

##### `default_settings.replica_auto_balance`

- Default value: `string`, `best-effort`

##### `default_settings.replicas`

- Default value: `integer`, `3`

Read the [Inventory Configuration](/k3s-cluster/wiki/guide/configuration/inventory/#configuration) guide, for more details.

{{% /steps %}}

#### `kubernetes.helm`

- Default value: `null`

{{% steps %}}

##### `helm.chart`

- Default value: `null`

{{% steps %}}

###### `chart.name`

- Default value: `string`, `longhorn`

###### `chart.version`

- Default value: `string`

Visit [`longhorn/longhorn`](https://github.com/longhorn/longhorn/releases), for latest release version.

{{% /steps %}}

##### `helm.repository`

- Default value: `null`

{{% steps %}}

###### `repository.name`

- Default value: `string`, `longhorn`

###### `repository.org`

- Default value: `string`, `longhorn`

###### `repository.url`

- Default value: `string`, `https://charts.longhorn.io`

{{% /steps %}}

{{% /steps %}}

#### `kubernetes.gateway`

- Default value: `null`

Read the [Gateway API](/k3s-cluster/tutorials/handbook/longhorn/#gateway-api) tutorial, for more details.

{{% steps %}}

##### `gateway.service`

- Default value: `string`, `longhorn-frontend`

##### `gateway.subdomain`

- Default value: `string`, `longhorn`

Sets the subdomain name for Longhorn UI.

{{% /steps %}}

#### `kubernetes.infrastructure`

- Default value: `null`

{{% steps %}}

##### `infrastructure.annotations`

- Default value: `map`

Sets the `infrastructure` [annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations).

{{% /steps %}}

#### `kubernetes.namespace`

- Default value: `string`, `kube-system`

#### `kubernetes.persistence`

- Default value: `null`

{{% steps %}}

##### `persistence.data_locality`

- Default value: `string`, `best-effort`

##### `persistence.migratable`

- Default value: `boolean`, `true`

##### `persistence.replicas`

- Default value: `integer`, `3`

Read the [Inventory Configuration](/k3s-cluster/wiki/guide/configuration/inventory/#configuration) guide, for more details.

{{% /steps %}}

{{% /steps %}}

{{% /steps %}}

## Role Tasks

See the related role tasks, listed below.

{{% steps %}}

### Facts

Ansible facts, see [`facts.yaml`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/tasks/facts.yaml) for details.

### Main

Main role related tasks, see [`main.yaml`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/tasks/main.yaml) for details.

### Reset

Reset related tasks, see [`reset.yaml`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/tasks/reset.yaml) for details.

### Validation

Validation related tasks, see [`validation.yaml`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/tasks/validation.yaml) for details.

{{% /steps %}}

## Role Templates

See the related role templates, listed below.

{{% steps %}}

### Helm Chart

Helm chart values template, see [`values.j2`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/templates/values.j2) for details.

### Gateway

Kubernetes `Gateway` resource template, see [`gateway.j2`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/templates/gateway.j2) for details.

### HTTP Route

{{% steps nested="true" %}}

#### Insecure Route

Kubernetes `HTTPRoute` resource template, see [`http_route.j2`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/templates/http_route.j2) for details.

#### Secure Route

Kubernetes `HTTPRoute` resource template, see [`https_route.j2`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/templates/https_route.j2) for details.

{{% /steps %}}

### Load Balancer

Kubernetes `Service` resource template, see [`loadbalancer.j2`](https://{{< param variables.repository.cluster >}}/blob/main/roles/longhorn/templates/loadbalancer.j2) for details.

{{% /steps %}}
