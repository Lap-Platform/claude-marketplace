---
name: kubernetes
description: "Kubernetes API skill. Use when working with Kubernetes for .well-known, api, apis. Covers 1085 endpoints."
version: 1.0.0
generator: lapsh
---

# Kubernetes
API version: unversioned

## Auth
ApiKey authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /.well-known/openid-configuration/ -- verify access
3. POST /api/v1/namespaces -- create first namespaces

## Endpoints

1085 endpoints across 6 groups. See references/api-spec.lap for full details.

### .well-known
| Method | Path | Description |
|--------|------|-------------|
| GET | /.well-known/openid-configuration/ | get service account issuer OpenID configuration, also known as the 'OIDC discovery doc' |

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/ | get available API versions |
| GET | /api/v1/ | get available resources |
| GET | /api/v1/componentstatuses | list objects of kind ComponentStatus |
| GET | /api/v1/componentstatuses/{name} | read the specified ComponentStatus |
| GET | /api/v1/configmaps | list or watch objects of kind ConfigMap |
| GET | /api/v1/endpoints | list or watch objects of kind Endpoints |
| GET | /api/v1/events | list or watch objects of kind Event |
| GET | /api/v1/limitranges | list or watch objects of kind LimitRange |
| GET | /api/v1/namespaces | list or watch objects of kind Namespace |
| POST | /api/v1/namespaces | create a Namespace |
| POST | /api/v1/namespaces/{namespace}/bindings | create a Binding |
| DELETE | /api/v1/namespaces/{namespace}/configmaps | delete collection of ConfigMap |
| GET | /api/v1/namespaces/{namespace}/configmaps | list or watch objects of kind ConfigMap |
| POST | /api/v1/namespaces/{namespace}/configmaps | create a ConfigMap |
| DELETE | /api/v1/namespaces/{namespace}/configmaps/{name} | delete a ConfigMap |
| GET | /api/v1/namespaces/{namespace}/configmaps/{name} | read the specified ConfigMap |
| PATCH | /api/v1/namespaces/{namespace}/configmaps/{name} | partially update the specified ConfigMap |
| PUT | /api/v1/namespaces/{namespace}/configmaps/{name} | replace the specified ConfigMap |
| DELETE | /api/v1/namespaces/{namespace}/endpoints | delete collection of Endpoints |
| GET | /api/v1/namespaces/{namespace}/endpoints | list or watch objects of kind Endpoints |
| POST | /api/v1/namespaces/{namespace}/endpoints | create Endpoints |
| DELETE | /api/v1/namespaces/{namespace}/endpoints/{name} | delete Endpoints |
| GET | /api/v1/namespaces/{namespace}/endpoints/{name} | read the specified Endpoints |
| PATCH | /api/v1/namespaces/{namespace}/endpoints/{name} | partially update the specified Endpoints |
| PUT | /api/v1/namespaces/{namespace}/endpoints/{name} | replace the specified Endpoints |
| DELETE | /api/v1/namespaces/{namespace}/events | delete collection of Event |
| GET | /api/v1/namespaces/{namespace}/events | list or watch objects of kind Event |
| POST | /api/v1/namespaces/{namespace}/events | create an Event |
| DELETE | /api/v1/namespaces/{namespace}/events/{name} | delete an Event |
| GET | /api/v1/namespaces/{namespace}/events/{name} | read the specified Event |
| PATCH | /api/v1/namespaces/{namespace}/events/{name} | partially update the specified Event |
| PUT | /api/v1/namespaces/{namespace}/events/{name} | replace the specified Event |
| DELETE | /api/v1/namespaces/{namespace}/limitranges | delete collection of LimitRange |
| GET | /api/v1/namespaces/{namespace}/limitranges | list or watch objects of kind LimitRange |
| POST | /api/v1/namespaces/{namespace}/limitranges | create a LimitRange |
| DELETE | /api/v1/namespaces/{namespace}/limitranges/{name} | delete a LimitRange |
| GET | /api/v1/namespaces/{namespace}/limitranges/{name} | read the specified LimitRange |
| PATCH | /api/v1/namespaces/{namespace}/limitranges/{name} | partially update the specified LimitRange |
| PUT | /api/v1/namespaces/{namespace}/limitranges/{name} | replace the specified LimitRange |
| DELETE | /api/v1/namespaces/{namespace}/persistentvolumeclaims | delete collection of PersistentVolumeClaim |
| GET | /api/v1/namespaces/{namespace}/persistentvolumeclaims | list or watch objects of kind PersistentVolumeClaim |
| POST | /api/v1/namespaces/{namespace}/persistentvolumeclaims | create a PersistentVolumeClaim |
| DELETE | /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name} | delete a PersistentVolumeClaim |
| GET | /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name} | read the specified PersistentVolumeClaim |
| PATCH | /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name} | partially update the specified PersistentVolumeClaim |
| PUT | /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name} | replace the specified PersistentVolumeClaim |
| GET | /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}/status | read status of the specified PersistentVolumeClaim |
| PATCH | /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}/status | partially update status of the specified PersistentVolumeClaim |
| PUT | /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}/status | replace status of the specified PersistentVolumeClaim |
| DELETE | /api/v1/namespaces/{namespace}/pods | delete collection of Pod |
| GET | /api/v1/namespaces/{namespace}/pods | list or watch objects of kind Pod |
| POST | /api/v1/namespaces/{namespace}/pods | create a Pod |
| DELETE | /api/v1/namespaces/{namespace}/pods/{name} | delete a Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name} | read the specified Pod |
| PATCH | /api/v1/namespaces/{namespace}/pods/{name} | partially update the specified Pod |
| PUT | /api/v1/namespaces/{namespace}/pods/{name} | replace the specified Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/attach | connect GET requests to attach of Pod |
| POST | /api/v1/namespaces/{namespace}/pods/{name}/attach | connect POST requests to attach of Pod |
| POST | /api/v1/namespaces/{namespace}/pods/{name}/binding | create binding of a Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/ephemeralcontainers | read ephemeralcontainers of the specified Pod |
| PATCH | /api/v1/namespaces/{namespace}/pods/{name}/ephemeralcontainers | partially update ephemeralcontainers of the specified Pod |
| PUT | /api/v1/namespaces/{namespace}/pods/{name}/ephemeralcontainers | replace ephemeralcontainers of the specified Pod |
| POST | /api/v1/namespaces/{namespace}/pods/{name}/eviction | create eviction of a Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/exec | connect GET requests to exec of Pod |
| POST | /api/v1/namespaces/{namespace}/pods/{name}/exec | connect POST requests to exec of Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/log | read log of the specified Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/portforward | connect GET requests to portforward of Pod |
| POST | /api/v1/namespaces/{namespace}/pods/{name}/portforward | connect POST requests to portforward of Pod |
| DELETE | /api/v1/namespaces/{namespace}/pods/{name}/proxy | connect DELETE requests to proxy of Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/proxy | connect GET requests to proxy of Pod |
| HEAD | /api/v1/namespaces/{namespace}/pods/{name}/proxy | connect HEAD requests to proxy of Pod |
| OPTIONS | /api/v1/namespaces/{namespace}/pods/{name}/proxy | connect OPTIONS requests to proxy of Pod |
| PATCH | /api/v1/namespaces/{namespace}/pods/{name}/proxy | connect PATCH requests to proxy of Pod |
| POST | /api/v1/namespaces/{namespace}/pods/{name}/proxy | connect POST requests to proxy of Pod |
| PUT | /api/v1/namespaces/{namespace}/pods/{name}/proxy | connect PUT requests to proxy of Pod |
| DELETE | /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path} | connect DELETE requests to proxy of Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path} | connect GET requests to proxy of Pod |
| HEAD | /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path} | connect HEAD requests to proxy of Pod |
| OPTIONS | /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path} | connect OPTIONS requests to proxy of Pod |
| PATCH | /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path} | connect PATCH requests to proxy of Pod |
| POST | /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path} | connect POST requests to proxy of Pod |
| PUT | /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path} | connect PUT requests to proxy of Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/resize | read resize of the specified Pod |
| PATCH | /api/v1/namespaces/{namespace}/pods/{name}/resize | partially update resize of the specified Pod |
| PUT | /api/v1/namespaces/{namespace}/pods/{name}/resize | replace resize of the specified Pod |
| GET | /api/v1/namespaces/{namespace}/pods/{name}/status | read status of the specified Pod |
| PATCH | /api/v1/namespaces/{namespace}/pods/{name}/status | partially update status of the specified Pod |
| PUT | /api/v1/namespaces/{namespace}/pods/{name}/status | replace status of the specified Pod |
| DELETE | /api/v1/namespaces/{namespace}/podtemplates | delete collection of PodTemplate |
| GET | /api/v1/namespaces/{namespace}/podtemplates | list or watch objects of kind PodTemplate |
| POST | /api/v1/namespaces/{namespace}/podtemplates | create a PodTemplate |
| DELETE | /api/v1/namespaces/{namespace}/podtemplates/{name} | delete a PodTemplate |
| GET | /api/v1/namespaces/{namespace}/podtemplates/{name} | read the specified PodTemplate |
| PATCH | /api/v1/namespaces/{namespace}/podtemplates/{name} | partially update the specified PodTemplate |
| PUT | /api/v1/namespaces/{namespace}/podtemplates/{name} | replace the specified PodTemplate |
| DELETE | /api/v1/namespaces/{namespace}/replicationcontrollers | delete collection of ReplicationController |
| GET | /api/v1/namespaces/{namespace}/replicationcontrollers | list or watch objects of kind ReplicationController |
| POST | /api/v1/namespaces/{namespace}/replicationcontrollers | create a ReplicationController |
| DELETE | /api/v1/namespaces/{namespace}/replicationcontrollers/{name} | delete a ReplicationController |
| GET | /api/v1/namespaces/{namespace}/replicationcontrollers/{name} | read the specified ReplicationController |
| PATCH | /api/v1/namespaces/{namespace}/replicationcontrollers/{name} | partially update the specified ReplicationController |
| PUT | /api/v1/namespaces/{namespace}/replicationcontrollers/{name} | replace the specified ReplicationController |
| GET | /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/scale | read scale of the specified ReplicationController |
| PATCH | /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/scale | partially update scale of the specified ReplicationController |
| PUT | /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/scale | replace scale of the specified ReplicationController |
| GET | /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/status | read status of the specified ReplicationController |
| PATCH | /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/status | partially update status of the specified ReplicationController |
| PUT | /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/status | replace status of the specified ReplicationController |
| DELETE | /api/v1/namespaces/{namespace}/resourcequotas | delete collection of ResourceQuota |
| GET | /api/v1/namespaces/{namespace}/resourcequotas | list or watch objects of kind ResourceQuota |
| POST | /api/v1/namespaces/{namespace}/resourcequotas | create a ResourceQuota |
| DELETE | /api/v1/namespaces/{namespace}/resourcequotas/{name} | delete a ResourceQuota |
| GET | /api/v1/namespaces/{namespace}/resourcequotas/{name} | read the specified ResourceQuota |
| PATCH | /api/v1/namespaces/{namespace}/resourcequotas/{name} | partially update the specified ResourceQuota |
| PUT | /api/v1/namespaces/{namespace}/resourcequotas/{name} | replace the specified ResourceQuota |
| GET | /api/v1/namespaces/{namespace}/resourcequotas/{name}/status | read status of the specified ResourceQuota |
| PATCH | /api/v1/namespaces/{namespace}/resourcequotas/{name}/status | partially update status of the specified ResourceQuota |
| PUT | /api/v1/namespaces/{namespace}/resourcequotas/{name}/status | replace status of the specified ResourceQuota |
| DELETE | /api/v1/namespaces/{namespace}/secrets | delete collection of Secret |
| GET | /api/v1/namespaces/{namespace}/secrets | list or watch objects of kind Secret |
| POST | /api/v1/namespaces/{namespace}/secrets | create a Secret |
| DELETE | /api/v1/namespaces/{namespace}/secrets/{name} | delete a Secret |
| GET | /api/v1/namespaces/{namespace}/secrets/{name} | read the specified Secret |
| PATCH | /api/v1/namespaces/{namespace}/secrets/{name} | partially update the specified Secret |
| PUT | /api/v1/namespaces/{namespace}/secrets/{name} | replace the specified Secret |
| DELETE | /api/v1/namespaces/{namespace}/serviceaccounts | delete collection of ServiceAccount |
| GET | /api/v1/namespaces/{namespace}/serviceaccounts | list or watch objects of kind ServiceAccount |
| POST | /api/v1/namespaces/{namespace}/serviceaccounts | create a ServiceAccount |
| DELETE | /api/v1/namespaces/{namespace}/serviceaccounts/{name} | delete a ServiceAccount |
| GET | /api/v1/namespaces/{namespace}/serviceaccounts/{name} | read the specified ServiceAccount |
| PATCH | /api/v1/namespaces/{namespace}/serviceaccounts/{name} | partially update the specified ServiceAccount |
| PUT | /api/v1/namespaces/{namespace}/serviceaccounts/{name} | replace the specified ServiceAccount |
| POST | /api/v1/namespaces/{namespace}/serviceaccounts/{name}/token | create token of a ServiceAccount |
| DELETE | /api/v1/namespaces/{namespace}/services | delete collection of Service |
| GET | /api/v1/namespaces/{namespace}/services | list or watch objects of kind Service |
| POST | /api/v1/namespaces/{namespace}/services | create a Service |
| DELETE | /api/v1/namespaces/{namespace}/services/{name} | delete a Service |
| GET | /api/v1/namespaces/{namespace}/services/{name} | read the specified Service |
| PATCH | /api/v1/namespaces/{namespace}/services/{name} | partially update the specified Service |
| PUT | /api/v1/namespaces/{namespace}/services/{name} | replace the specified Service |
| DELETE | /api/v1/namespaces/{namespace}/services/{name}/proxy | connect DELETE requests to proxy of Service |
| GET | /api/v1/namespaces/{namespace}/services/{name}/proxy | connect GET requests to proxy of Service |
| HEAD | /api/v1/namespaces/{namespace}/services/{name}/proxy | connect HEAD requests to proxy of Service |
| OPTIONS | /api/v1/namespaces/{namespace}/services/{name}/proxy | connect OPTIONS requests to proxy of Service |
| PATCH | /api/v1/namespaces/{namespace}/services/{name}/proxy | connect PATCH requests to proxy of Service |
| POST | /api/v1/namespaces/{namespace}/services/{name}/proxy | connect POST requests to proxy of Service |
| PUT | /api/v1/namespaces/{namespace}/services/{name}/proxy | connect PUT requests to proxy of Service |
| DELETE | /api/v1/namespaces/{namespace}/services/{name}/proxy/{path} | connect DELETE requests to proxy of Service |
| GET | /api/v1/namespaces/{namespace}/services/{name}/proxy/{path} | connect GET requests to proxy of Service |
| HEAD | /api/v1/namespaces/{namespace}/services/{name}/proxy/{path} | connect HEAD requests to proxy of Service |
| OPTIONS | /api/v1/namespaces/{namespace}/services/{name}/proxy/{path} | connect OPTIONS requests to proxy of Service |
| PATCH | /api/v1/namespaces/{namespace}/services/{name}/proxy/{path} | connect PATCH requests to proxy of Service |
| POST | /api/v1/namespaces/{namespace}/services/{name}/proxy/{path} | connect POST requests to proxy of Service |
| PUT | /api/v1/namespaces/{namespace}/services/{name}/proxy/{path} | connect PUT requests to proxy of Service |
| GET | /api/v1/namespaces/{namespace}/services/{name}/status | read status of the specified Service |
| PATCH | /api/v1/namespaces/{namespace}/services/{name}/status | partially update status of the specified Service |
| PUT | /api/v1/namespaces/{namespace}/services/{name}/status | replace status of the specified Service |
| DELETE | /api/v1/namespaces/{name} | delete a Namespace |
| GET | /api/v1/namespaces/{name} | read the specified Namespace |
| PATCH | /api/v1/namespaces/{name} | partially update the specified Namespace |
| PUT | /api/v1/namespaces/{name} | replace the specified Namespace |
| PUT | /api/v1/namespaces/{name}/finalize | replace finalize of the specified Namespace |
| GET | /api/v1/namespaces/{name}/status | read status of the specified Namespace |
| PATCH | /api/v1/namespaces/{name}/status | partially update status of the specified Namespace |
| PUT | /api/v1/namespaces/{name}/status | replace status of the specified Namespace |
| DELETE | /api/v1/nodes | delete collection of Node |
| GET | /api/v1/nodes | list or watch objects of kind Node |
| POST | /api/v1/nodes | create a Node |
| DELETE | /api/v1/nodes/{name} | delete a Node |
| GET | /api/v1/nodes/{name} | read the specified Node |
| PATCH | /api/v1/nodes/{name} | partially update the specified Node |
| PUT | /api/v1/nodes/{name} | replace the specified Node |
| DELETE | /api/v1/nodes/{name}/proxy | connect DELETE requests to proxy of Node |
| GET | /api/v1/nodes/{name}/proxy | connect GET requests to proxy of Node |
| HEAD | /api/v1/nodes/{name}/proxy | connect HEAD requests to proxy of Node |
| OPTIONS | /api/v1/nodes/{name}/proxy | connect OPTIONS requests to proxy of Node |
| PATCH | /api/v1/nodes/{name}/proxy | connect PATCH requests to proxy of Node |
| POST | /api/v1/nodes/{name}/proxy | connect POST requests to proxy of Node |
| PUT | /api/v1/nodes/{name}/proxy | connect PUT requests to proxy of Node |
| DELETE | /api/v1/nodes/{name}/proxy/{path} | connect DELETE requests to proxy of Node |
| GET | /api/v1/nodes/{name}/proxy/{path} | connect GET requests to proxy of Node |
| HEAD | /api/v1/nodes/{name}/proxy/{path} | connect HEAD requests to proxy of Node |
| OPTIONS | /api/v1/nodes/{name}/proxy/{path} | connect OPTIONS requests to proxy of Node |
| PATCH | /api/v1/nodes/{name}/proxy/{path} | connect PATCH requests to proxy of Node |
| POST | /api/v1/nodes/{name}/proxy/{path} | connect POST requests to proxy of Node |
| PUT | /api/v1/nodes/{name}/proxy/{path} | connect PUT requests to proxy of Node |
| GET | /api/v1/nodes/{name}/status | read status of the specified Node |
| PATCH | /api/v1/nodes/{name}/status | partially update status of the specified Node |
| PUT | /api/v1/nodes/{name}/status | replace status of the specified Node |
| GET | /api/v1/persistentvolumeclaims | list or watch objects of kind PersistentVolumeClaim |
| DELETE | /api/v1/persistentvolumes | delete collection of PersistentVolume |
| GET | /api/v1/persistentvolumes | list or watch objects of kind PersistentVolume |
| POST | /api/v1/persistentvolumes | create a PersistentVolume |
| DELETE | /api/v1/persistentvolumes/{name} | delete a PersistentVolume |
| GET | /api/v1/persistentvolumes/{name} | read the specified PersistentVolume |
| PATCH | /api/v1/persistentvolumes/{name} | partially update the specified PersistentVolume |
| PUT | /api/v1/persistentvolumes/{name} | replace the specified PersistentVolume |
| GET | /api/v1/persistentvolumes/{name}/status | read status of the specified PersistentVolume |
| PATCH | /api/v1/persistentvolumes/{name}/status | partially update status of the specified PersistentVolume |
| PUT | /api/v1/persistentvolumes/{name}/status | replace status of the specified PersistentVolume |
| GET | /api/v1/pods | list or watch objects of kind Pod |
| GET | /api/v1/podtemplates | list or watch objects of kind PodTemplate |
| GET | /api/v1/replicationcontrollers | list or watch objects of kind ReplicationController |
| GET | /api/v1/resourcequotas | list or watch objects of kind ResourceQuota |
| GET | /api/v1/secrets | list or watch objects of kind Secret |
| GET | /api/v1/serviceaccounts | list or watch objects of kind ServiceAccount |
| GET | /api/v1/services | list or watch objects of kind Service |
| GET | /api/v1/watch/configmaps | watch individual changes to a list of ConfigMap. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/endpoints | watch individual changes to a list of Endpoints. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/events | watch individual changes to a list of Event. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/limitranges | watch individual changes to a list of LimitRange. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces | watch individual changes to a list of Namespace. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/configmaps | watch individual changes to a list of ConfigMap. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/configmaps/{name} | watch changes to an object of kind ConfigMap. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/endpoints | watch individual changes to a list of Endpoints. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/endpoints/{name} | watch changes to an object of kind Endpoints. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/events | watch individual changes to a list of Event. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/events/{name} | watch changes to an object of kind Event. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/limitranges | watch individual changes to a list of LimitRange. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/limitranges/{name} | watch changes to an object of kind LimitRange. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/persistentvolumeclaims | watch individual changes to a list of PersistentVolumeClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/persistentvolumeclaims/{name} | watch changes to an object of kind PersistentVolumeClaim. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/pods | watch individual changes to a list of Pod. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/pods/{name} | watch changes to an object of kind Pod. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/podtemplates | watch individual changes to a list of PodTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/podtemplates/{name} | watch changes to an object of kind PodTemplate. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/replicationcontrollers | watch individual changes to a list of ReplicationController. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/replicationcontrollers/{name} | watch changes to an object of kind ReplicationController. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/resourcequotas | watch individual changes to a list of ResourceQuota. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/resourcequotas/{name} | watch changes to an object of kind ResourceQuota. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/secrets | watch individual changes to a list of Secret. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/secrets/{name} | watch changes to an object of kind Secret. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/serviceaccounts | watch individual changes to a list of ServiceAccount. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/serviceaccounts/{name} | watch changes to an object of kind ServiceAccount. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{namespace}/services | watch individual changes to a list of Service. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/namespaces/{namespace}/services/{name} | watch changes to an object of kind Service. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/namespaces/{name} | watch changes to an object of kind Namespace. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/nodes | watch individual changes to a list of Node. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/nodes/{name} | watch changes to an object of kind Node. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/persistentvolumeclaims | watch individual changes to a list of PersistentVolumeClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/persistentvolumes | watch individual changes to a list of PersistentVolume. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/persistentvolumes/{name} | watch changes to an object of kind PersistentVolume. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /api/v1/watch/pods | watch individual changes to a list of Pod. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/podtemplates | watch individual changes to a list of PodTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/replicationcontrollers | watch individual changes to a list of ReplicationController. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/resourcequotas | watch individual changes to a list of ResourceQuota. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/secrets | watch individual changes to a list of Secret. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/serviceaccounts | watch individual changes to a list of ServiceAccount. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /api/v1/watch/services | watch individual changes to a list of Service. deprecated: use the 'watch' parameter with a list operation instead. |

### apis
| Method | Path | Description |
|--------|------|-------------|
| GET | /apis/ | get available API versions |
| GET | /apis/admissionregistration.k8s.io/ | get information of a group |
| GET | /apis/admissionregistration.k8s.io/v1/ | get available resources |
| DELETE | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies | delete collection of MutatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies | list or watch objects of kind MutatingAdmissionPolicy |
| POST | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies | create a MutatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name} | delete a MutatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name} | read the specified MutatingAdmissionPolicy |
| PATCH | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name} | partially update the specified MutatingAdmissionPolicy |
| PUT | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name} | replace the specified MutatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings | delete collection of MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings | list or watch objects of kind MutatingAdmissionPolicyBinding |
| POST | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings | create a MutatingAdmissionPolicyBinding |
| DELETE | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name} | delete a MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name} | read the specified MutatingAdmissionPolicyBinding |
| PATCH | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name} | partially update the specified MutatingAdmissionPolicyBinding |
| PUT | /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name} | replace the specified MutatingAdmissionPolicyBinding |
| DELETE | /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations | delete collection of MutatingWebhookConfiguration |
| GET | /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations | list or watch objects of kind MutatingWebhookConfiguration |
| POST | /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations | create a MutatingWebhookConfiguration |
| DELETE | /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name} | delete a MutatingWebhookConfiguration |
| GET | /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name} | read the specified MutatingWebhookConfiguration |
| PATCH | /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name} | partially update the specified MutatingWebhookConfiguration |
| PUT | /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name} | replace the specified MutatingWebhookConfiguration |
| DELETE | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies | delete collection of ValidatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies | list or watch objects of kind ValidatingAdmissionPolicy |
| POST | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies | create a ValidatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name} | delete a ValidatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name} | read the specified ValidatingAdmissionPolicy |
| PATCH | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name} | partially update the specified ValidatingAdmissionPolicy |
| PUT | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name} | replace the specified ValidatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}/status | read status of the specified ValidatingAdmissionPolicy |
| PATCH | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}/status | partially update status of the specified ValidatingAdmissionPolicy |
| PUT | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}/status | replace status of the specified ValidatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings | delete collection of ValidatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings | list or watch objects of kind ValidatingAdmissionPolicyBinding |
| POST | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings | create a ValidatingAdmissionPolicyBinding |
| DELETE | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name} | delete a ValidatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name} | read the specified ValidatingAdmissionPolicyBinding |
| PATCH | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name} | partially update the specified ValidatingAdmissionPolicyBinding |
| PUT | /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name} | replace the specified ValidatingAdmissionPolicyBinding |
| DELETE | /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations | delete collection of ValidatingWebhookConfiguration |
| GET | /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations | list or watch objects of kind ValidatingWebhookConfiguration |
| POST | /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations | create a ValidatingWebhookConfiguration |
| DELETE | /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name} | delete a ValidatingWebhookConfiguration |
| GET | /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name} | read the specified ValidatingWebhookConfiguration |
| PATCH | /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name} | partially update the specified ValidatingWebhookConfiguration |
| PUT | /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name} | replace the specified ValidatingWebhookConfiguration |
| GET | /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicies | watch individual changes to a list of MutatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicies/{name} | watch changes to an object of kind MutatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicybindings | watch individual changes to a list of MutatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicybindings/{name} | watch changes to an object of kind MutatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/mutatingwebhookconfigurations | watch individual changes to a list of MutatingWebhookConfiguration. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/mutatingwebhookconfigurations/{name} | watch changes to an object of kind MutatingWebhookConfiguration. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicies | watch individual changes to a list of ValidatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicies/{name} | watch changes to an object of kind ValidatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicybindings | watch individual changes to a list of ValidatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicybindings/{name} | watch changes to an object of kind ValidatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/validatingwebhookconfigurations | watch individual changes to a list of ValidatingWebhookConfiguration. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1/watch/validatingwebhookconfigurations/{name} | watch changes to an object of kind ValidatingWebhookConfiguration. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/ | get available resources |
| DELETE | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies | delete collection of MutatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies | list or watch objects of kind MutatingAdmissionPolicy |
| POST | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies | create a MutatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name} | delete a MutatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name} | read the specified MutatingAdmissionPolicy |
| PATCH | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name} | partially update the specified MutatingAdmissionPolicy |
| PUT | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name} | replace the specified MutatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings | delete collection of MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings | list or watch objects of kind MutatingAdmissionPolicyBinding |
| POST | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings | create a MutatingAdmissionPolicyBinding |
| DELETE | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name} | delete a MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name} | read the specified MutatingAdmissionPolicyBinding |
| PATCH | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name} | partially update the specified MutatingAdmissionPolicyBinding |
| PUT | /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name} | replace the specified MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicies | watch individual changes to a list of MutatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicies/{name} | watch changes to an object of kind MutatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicybindings | watch individual changes to a list of MutatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicybindings/{name} | watch changes to an object of kind MutatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1beta1/ | get available resources |
| DELETE | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies | delete collection of MutatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies | list or watch objects of kind MutatingAdmissionPolicy |
| POST | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies | create a MutatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name} | delete a MutatingAdmissionPolicy |
| GET | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name} | read the specified MutatingAdmissionPolicy |
| PATCH | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name} | partially update the specified MutatingAdmissionPolicy |
| PUT | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name} | replace the specified MutatingAdmissionPolicy |
| DELETE | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings | delete collection of MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings | list or watch objects of kind MutatingAdmissionPolicyBinding |
| POST | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings | create a MutatingAdmissionPolicyBinding |
| DELETE | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name} | delete a MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name} | read the specified MutatingAdmissionPolicyBinding |
| PATCH | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name} | partially update the specified MutatingAdmissionPolicyBinding |
| PUT | /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name} | replace the specified MutatingAdmissionPolicyBinding |
| GET | /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicies | watch individual changes to a list of MutatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicies/{name} | watch changes to an object of kind MutatingAdmissionPolicy. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicybindings | watch individual changes to a list of MutatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicybindings/{name} | watch changes to an object of kind MutatingAdmissionPolicyBinding. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apiextensions.k8s.io/ | get information of a group |
| GET | /apis/apiextensions.k8s.io/v1/ | get available resources |
| DELETE | /apis/apiextensions.k8s.io/v1/customresourcedefinitions | delete collection of CustomResourceDefinition |
| GET | /apis/apiextensions.k8s.io/v1/customresourcedefinitions | list or watch objects of kind CustomResourceDefinition |
| POST | /apis/apiextensions.k8s.io/v1/customresourcedefinitions | create a CustomResourceDefinition |
| DELETE | /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name} | delete a CustomResourceDefinition |
| GET | /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name} | read the specified CustomResourceDefinition |
| PATCH | /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name} | partially update the specified CustomResourceDefinition |
| PUT | /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name} | replace the specified CustomResourceDefinition |
| GET | /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}/status | read status of the specified CustomResourceDefinition |
| PATCH | /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}/status | partially update status of the specified CustomResourceDefinition |
| PUT | /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}/status | replace status of the specified CustomResourceDefinition |
| GET | /apis/apiextensions.k8s.io/v1/watch/customresourcedefinitions | watch individual changes to a list of CustomResourceDefinition. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apiextensions.k8s.io/v1/watch/customresourcedefinitions/{name} | watch changes to an object of kind CustomResourceDefinition. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apiregistration.k8s.io/ | get information of a group |
| GET | /apis/apiregistration.k8s.io/v1/ | get available resources |
| DELETE | /apis/apiregistration.k8s.io/v1/apiservices | delete collection of APIService |
| GET | /apis/apiregistration.k8s.io/v1/apiservices | list or watch objects of kind APIService |
| POST | /apis/apiregistration.k8s.io/v1/apiservices | create an APIService |
| DELETE | /apis/apiregistration.k8s.io/v1/apiservices/{name} | delete an APIService |
| GET | /apis/apiregistration.k8s.io/v1/apiservices/{name} | read the specified APIService |
| PATCH | /apis/apiregistration.k8s.io/v1/apiservices/{name} | partially update the specified APIService |
| PUT | /apis/apiregistration.k8s.io/v1/apiservices/{name} | replace the specified APIService |
| GET | /apis/apiregistration.k8s.io/v1/apiservices/{name}/status | read status of the specified APIService |
| PATCH | /apis/apiregistration.k8s.io/v1/apiservices/{name}/status | partially update status of the specified APIService |
| PUT | /apis/apiregistration.k8s.io/v1/apiservices/{name}/status | replace status of the specified APIService |
| GET | /apis/apiregistration.k8s.io/v1/watch/apiservices | watch individual changes to a list of APIService. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apiregistration.k8s.io/v1/watch/apiservices/{name} | watch changes to an object of kind APIService. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apps/ | get information of a group |
| GET | /apis/apps/v1/ | get available resources |
| GET | /apis/apps/v1/controllerrevisions | list or watch objects of kind ControllerRevision |
| GET | /apis/apps/v1/daemonsets | list or watch objects of kind DaemonSet |
| GET | /apis/apps/v1/deployments | list or watch objects of kind Deployment |
| DELETE | /apis/apps/v1/namespaces/{namespace}/controllerrevisions | delete collection of ControllerRevision |
| GET | /apis/apps/v1/namespaces/{namespace}/controllerrevisions | list or watch objects of kind ControllerRevision |
| POST | /apis/apps/v1/namespaces/{namespace}/controllerrevisions | create a ControllerRevision |
| DELETE | /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name} | delete a ControllerRevision |
| GET | /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name} | read the specified ControllerRevision |
| PATCH | /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name} | partially update the specified ControllerRevision |
| PUT | /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name} | replace the specified ControllerRevision |
| DELETE | /apis/apps/v1/namespaces/{namespace}/daemonsets | delete collection of DaemonSet |
| GET | /apis/apps/v1/namespaces/{namespace}/daemonsets | list or watch objects of kind DaemonSet |
| POST | /apis/apps/v1/namespaces/{namespace}/daemonsets | create a DaemonSet |
| DELETE | /apis/apps/v1/namespaces/{namespace}/daemonsets/{name} | delete a DaemonSet |
| GET | /apis/apps/v1/namespaces/{namespace}/daemonsets/{name} | read the specified DaemonSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/daemonsets/{name} | partially update the specified DaemonSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/daemonsets/{name} | replace the specified DaemonSet |
| GET | /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}/status | read status of the specified DaemonSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}/status | partially update status of the specified DaemonSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}/status | replace status of the specified DaemonSet |
| DELETE | /apis/apps/v1/namespaces/{namespace}/deployments | delete collection of Deployment |
| GET | /apis/apps/v1/namespaces/{namespace}/deployments | list or watch objects of kind Deployment |
| POST | /apis/apps/v1/namespaces/{namespace}/deployments | create a Deployment |
| DELETE | /apis/apps/v1/namespaces/{namespace}/deployments/{name} | delete a Deployment |
| GET | /apis/apps/v1/namespaces/{namespace}/deployments/{name} | read the specified Deployment |
| PATCH | /apis/apps/v1/namespaces/{namespace}/deployments/{name} | partially update the specified Deployment |
| PUT | /apis/apps/v1/namespaces/{namespace}/deployments/{name} | replace the specified Deployment |
| GET | /apis/apps/v1/namespaces/{namespace}/deployments/{name}/scale | read scale of the specified Deployment |
| PATCH | /apis/apps/v1/namespaces/{namespace}/deployments/{name}/scale | partially update scale of the specified Deployment |
| PUT | /apis/apps/v1/namespaces/{namespace}/deployments/{name}/scale | replace scale of the specified Deployment |
| GET | /apis/apps/v1/namespaces/{namespace}/deployments/{name}/status | read status of the specified Deployment |
| PATCH | /apis/apps/v1/namespaces/{namespace}/deployments/{name}/status | partially update status of the specified Deployment |
| PUT | /apis/apps/v1/namespaces/{namespace}/deployments/{name}/status | replace status of the specified Deployment |
| DELETE | /apis/apps/v1/namespaces/{namespace}/replicasets | delete collection of ReplicaSet |
| GET | /apis/apps/v1/namespaces/{namespace}/replicasets | list or watch objects of kind ReplicaSet |
| POST | /apis/apps/v1/namespaces/{namespace}/replicasets | create a ReplicaSet |
| DELETE | /apis/apps/v1/namespaces/{namespace}/replicasets/{name} | delete a ReplicaSet |
| GET | /apis/apps/v1/namespaces/{namespace}/replicasets/{name} | read the specified ReplicaSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/replicasets/{name} | partially update the specified ReplicaSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/replicasets/{name} | replace the specified ReplicaSet |
| GET | /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/scale | read scale of the specified ReplicaSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/scale | partially update scale of the specified ReplicaSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/scale | replace scale of the specified ReplicaSet |
| GET | /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/status | read status of the specified ReplicaSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/status | partially update status of the specified ReplicaSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/status | replace status of the specified ReplicaSet |
| DELETE | /apis/apps/v1/namespaces/{namespace}/statefulsets | delete collection of StatefulSet |
| GET | /apis/apps/v1/namespaces/{namespace}/statefulsets | list or watch objects of kind StatefulSet |
| POST | /apis/apps/v1/namespaces/{namespace}/statefulsets | create a StatefulSet |
| DELETE | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name} | delete a StatefulSet |
| GET | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name} | read the specified StatefulSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name} | partially update the specified StatefulSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name} | replace the specified StatefulSet |
| GET | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/scale | read scale of the specified StatefulSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/scale | partially update scale of the specified StatefulSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/scale | replace scale of the specified StatefulSet |
| GET | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/status | read status of the specified StatefulSet |
| PATCH | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/status | partially update status of the specified StatefulSet |
| PUT | /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/status | replace status of the specified StatefulSet |
| GET | /apis/apps/v1/replicasets | list or watch objects of kind ReplicaSet |
| GET | /apis/apps/v1/statefulsets | list or watch objects of kind StatefulSet |
| GET | /apis/apps/v1/watch/controllerrevisions | watch individual changes to a list of ControllerRevision. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/daemonsets | watch individual changes to a list of DaemonSet. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/deployments | watch individual changes to a list of Deployment. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/controllerrevisions | watch individual changes to a list of ControllerRevision. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/controllerrevisions/{name} | watch changes to an object of kind ControllerRevision. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/daemonsets | watch individual changes to a list of DaemonSet. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/daemonsets/{name} | watch changes to an object of kind DaemonSet. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/deployments | watch individual changes to a list of Deployment. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/deployments/{name} | watch changes to an object of kind Deployment. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/replicasets | watch individual changes to a list of ReplicaSet. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/replicasets/{name} | watch changes to an object of kind ReplicaSet. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/statefulsets | watch individual changes to a list of StatefulSet. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/namespaces/{namespace}/statefulsets/{name} | watch changes to an object of kind StatefulSet. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/apps/v1/watch/replicasets | watch individual changes to a list of ReplicaSet. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/apps/v1/watch/statefulsets | watch individual changes to a list of StatefulSet. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/authentication.k8s.io/ | get information of a group |
| GET | /apis/authentication.k8s.io/v1/ | get available resources |
| POST | /apis/authentication.k8s.io/v1/selfsubjectreviews | create a SelfSubjectReview |
| POST | /apis/authentication.k8s.io/v1/tokenreviews | create a TokenReview |
| GET | /apis/authorization.k8s.io/ | get information of a group |
| GET | /apis/authorization.k8s.io/v1/ | get available resources |
| POST | /apis/authorization.k8s.io/v1/namespaces/{namespace}/localsubjectaccessreviews | create a LocalSubjectAccessReview |
| POST | /apis/authorization.k8s.io/v1/selfsubjectaccessreviews | create a SelfSubjectAccessReview |
| POST | /apis/authorization.k8s.io/v1/selfsubjectrulesreviews | create a SelfSubjectRulesReview |
| POST | /apis/authorization.k8s.io/v1/subjectaccessreviews | create a SubjectAccessReview |
| GET | /apis/autoscaling/ | get information of a group |
| GET | /apis/autoscaling/v1/ | get available resources |
| GET | /apis/autoscaling/v1/horizontalpodautoscalers | list or watch objects of kind HorizontalPodAutoscaler |
| DELETE | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers | delete collection of HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers | list or watch objects of kind HorizontalPodAutoscaler |
| POST | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers | create a HorizontalPodAutoscaler |
| DELETE | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name} | delete a HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name} | read the specified HorizontalPodAutoscaler |
| PATCH | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name} | partially update the specified HorizontalPodAutoscaler |
| PUT | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name} | replace the specified HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}/status | read status of the specified HorizontalPodAutoscaler |
| PATCH | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}/status | partially update status of the specified HorizontalPodAutoscaler |
| PUT | /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}/status | replace status of the specified HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v1/watch/horizontalpodautoscalers | watch individual changes to a list of HorizontalPodAutoscaler. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/autoscaling/v1/watch/namespaces/{namespace}/horizontalpodautoscalers | watch individual changes to a list of HorizontalPodAutoscaler. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/autoscaling/v1/watch/namespaces/{namespace}/horizontalpodautoscalers/{name} | watch changes to an object of kind HorizontalPodAutoscaler. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/autoscaling/v2/ | get available resources |
| GET | /apis/autoscaling/v2/horizontalpodautoscalers | list or watch objects of kind HorizontalPodAutoscaler |
| DELETE | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers | delete collection of HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers | list or watch objects of kind HorizontalPodAutoscaler |
| POST | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers | create a HorizontalPodAutoscaler |
| DELETE | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name} | delete a HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name} | read the specified HorizontalPodAutoscaler |
| PATCH | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name} | partially update the specified HorizontalPodAutoscaler |
| PUT | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name} | replace the specified HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}/status | read status of the specified HorizontalPodAutoscaler |
| PATCH | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}/status | partially update status of the specified HorizontalPodAutoscaler |
| PUT | /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}/status | replace status of the specified HorizontalPodAutoscaler |
| GET | /apis/autoscaling/v2/watch/horizontalpodautoscalers | watch individual changes to a list of HorizontalPodAutoscaler. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/autoscaling/v2/watch/namespaces/{namespace}/horizontalpodautoscalers | watch individual changes to a list of HorizontalPodAutoscaler. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/autoscaling/v2/watch/namespaces/{namespace}/horizontalpodautoscalers/{name} | watch changes to an object of kind HorizontalPodAutoscaler. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/batch/ | get information of a group |
| GET | /apis/batch/v1/ | get available resources |
| GET | /apis/batch/v1/cronjobs | list or watch objects of kind CronJob |
| GET | /apis/batch/v1/jobs | list or watch objects of kind Job |
| DELETE | /apis/batch/v1/namespaces/{namespace}/cronjobs | delete collection of CronJob |
| GET | /apis/batch/v1/namespaces/{namespace}/cronjobs | list or watch objects of kind CronJob |
| POST | /apis/batch/v1/namespaces/{namespace}/cronjobs | create a CronJob |
| DELETE | /apis/batch/v1/namespaces/{namespace}/cronjobs/{name} | delete a CronJob |
| GET | /apis/batch/v1/namespaces/{namespace}/cronjobs/{name} | read the specified CronJob |
| PATCH | /apis/batch/v1/namespaces/{namespace}/cronjobs/{name} | partially update the specified CronJob |
| PUT | /apis/batch/v1/namespaces/{namespace}/cronjobs/{name} | replace the specified CronJob |
| GET | /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}/status | read status of the specified CronJob |
| PATCH | /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}/status | partially update status of the specified CronJob |
| PUT | /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}/status | replace status of the specified CronJob |
| DELETE | /apis/batch/v1/namespaces/{namespace}/jobs | delete collection of Job |
| GET | /apis/batch/v1/namespaces/{namespace}/jobs | list or watch objects of kind Job |
| POST | /apis/batch/v1/namespaces/{namespace}/jobs | create a Job |
| DELETE | /apis/batch/v1/namespaces/{namespace}/jobs/{name} | delete a Job |
| GET | /apis/batch/v1/namespaces/{namespace}/jobs/{name} | read the specified Job |
| PATCH | /apis/batch/v1/namespaces/{namespace}/jobs/{name} | partially update the specified Job |
| PUT | /apis/batch/v1/namespaces/{namespace}/jobs/{name} | replace the specified Job |
| GET | /apis/batch/v1/namespaces/{namespace}/jobs/{name}/status | read status of the specified Job |
| PATCH | /apis/batch/v1/namespaces/{namespace}/jobs/{name}/status | partially update status of the specified Job |
| PUT | /apis/batch/v1/namespaces/{namespace}/jobs/{name}/status | replace status of the specified Job |
| GET | /apis/batch/v1/watch/cronjobs | watch individual changes to a list of CronJob. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/batch/v1/watch/jobs | watch individual changes to a list of Job. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/batch/v1/watch/namespaces/{namespace}/cronjobs | watch individual changes to a list of CronJob. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/batch/v1/watch/namespaces/{namespace}/cronjobs/{name} | watch changes to an object of kind CronJob. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/batch/v1/watch/namespaces/{namespace}/jobs | watch individual changes to a list of Job. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/batch/v1/watch/namespaces/{namespace}/jobs/{name} | watch changes to an object of kind Job. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/certificates.k8s.io/ | get information of a group |
| GET | /apis/certificates.k8s.io/v1/ | get available resources |
| DELETE | /apis/certificates.k8s.io/v1/certificatesigningrequests | delete collection of CertificateSigningRequest |
| GET | /apis/certificates.k8s.io/v1/certificatesigningrequests | list or watch objects of kind CertificateSigningRequest |
| POST | /apis/certificates.k8s.io/v1/certificatesigningrequests | create a CertificateSigningRequest |
| DELETE | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name} | delete a CertificateSigningRequest |
| GET | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name} | read the specified CertificateSigningRequest |
| PATCH | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name} | partially update the specified CertificateSigningRequest |
| PUT | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name} | replace the specified CertificateSigningRequest |
| GET | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/approval | read approval of the specified CertificateSigningRequest |
| PATCH | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/approval | partially update approval of the specified CertificateSigningRequest |
| PUT | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/approval | replace approval of the specified CertificateSigningRequest |
| GET | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/status | read status of the specified CertificateSigningRequest |
| PATCH | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/status | partially update status of the specified CertificateSigningRequest |
| PUT | /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/status | replace status of the specified CertificateSigningRequest |
| GET | /apis/certificates.k8s.io/v1/watch/certificatesigningrequests | watch individual changes to a list of CertificateSigningRequest. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/certificates.k8s.io/v1/watch/certificatesigningrequests/{name} | watch changes to an object of kind CertificateSigningRequest. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/certificates.k8s.io/v1alpha1/ | get available resources |
| DELETE | /apis/certificates.k8s.io/v1alpha1/clustertrustbundles | delete collection of ClusterTrustBundle |
| GET | /apis/certificates.k8s.io/v1alpha1/clustertrustbundles | list or watch objects of kind ClusterTrustBundle |
| POST | /apis/certificates.k8s.io/v1alpha1/clustertrustbundles | create a ClusterTrustBundle |
| DELETE | /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name} | delete a ClusterTrustBundle |
| GET | /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name} | read the specified ClusterTrustBundle |
| PATCH | /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name} | partially update the specified ClusterTrustBundle |
| PUT | /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name} | replace the specified ClusterTrustBundle |
| GET | /apis/certificates.k8s.io/v1alpha1/watch/clustertrustbundles | watch individual changes to a list of ClusterTrustBundle. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/certificates.k8s.io/v1alpha1/watch/clustertrustbundles/{name} | watch changes to an object of kind ClusterTrustBundle. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/certificates.k8s.io/v1beta1/ | get available resources |
| DELETE | /apis/certificates.k8s.io/v1beta1/clustertrustbundles | delete collection of ClusterTrustBundle |
| GET | /apis/certificates.k8s.io/v1beta1/clustertrustbundles | list or watch objects of kind ClusterTrustBundle |
| POST | /apis/certificates.k8s.io/v1beta1/clustertrustbundles | create a ClusterTrustBundle |
| DELETE | /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name} | delete a ClusterTrustBundle |
| GET | /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name} | read the specified ClusterTrustBundle |
| PATCH | /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name} | partially update the specified ClusterTrustBundle |
| PUT | /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name} | replace the specified ClusterTrustBundle |
| DELETE | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests | delete collection of PodCertificateRequest |
| GET | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests | list or watch objects of kind PodCertificateRequest |
| POST | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests | create a PodCertificateRequest |
| DELETE | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name} | delete a PodCertificateRequest |
| GET | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name} | read the specified PodCertificateRequest |
| PATCH | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name} | partially update the specified PodCertificateRequest |
| PUT | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name} | replace the specified PodCertificateRequest |
| GET | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}/status | read status of the specified PodCertificateRequest |
| PATCH | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}/status | partially update status of the specified PodCertificateRequest |
| PUT | /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}/status | replace status of the specified PodCertificateRequest |
| GET | /apis/certificates.k8s.io/v1beta1/podcertificaterequests | list or watch objects of kind PodCertificateRequest |
| GET | /apis/certificates.k8s.io/v1beta1/watch/clustertrustbundles | watch individual changes to a list of ClusterTrustBundle. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/certificates.k8s.io/v1beta1/watch/clustertrustbundles/{name} | watch changes to an object of kind ClusterTrustBundle. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/certificates.k8s.io/v1beta1/watch/namespaces/{namespace}/podcertificaterequests | watch individual changes to a list of PodCertificateRequest. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/certificates.k8s.io/v1beta1/watch/namespaces/{namespace}/podcertificaterequests/{name} | watch changes to an object of kind PodCertificateRequest. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/certificates.k8s.io/v1beta1/watch/podcertificaterequests | watch individual changes to a list of PodCertificateRequest. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/coordination.k8s.io/ | get information of a group |
| GET | /apis/coordination.k8s.io/v1/ | get available resources |
| GET | /apis/coordination.k8s.io/v1/leases | list or watch objects of kind Lease |
| DELETE | /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases | delete collection of Lease |
| GET | /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases | list or watch objects of kind Lease |
| POST | /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases | create a Lease |
| DELETE | /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name} | delete a Lease |
| GET | /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name} | read the specified Lease |
| PATCH | /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name} | partially update the specified Lease |
| PUT | /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name} | replace the specified Lease |
| GET | /apis/coordination.k8s.io/v1/watch/leases | watch individual changes to a list of Lease. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/coordination.k8s.io/v1/watch/namespaces/{namespace}/leases | watch individual changes to a list of Lease. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/coordination.k8s.io/v1/watch/namespaces/{namespace}/leases/{name} | watch changes to an object of kind Lease. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/coordination.k8s.io/v1alpha2/ | get available resources |
| GET | /apis/coordination.k8s.io/v1alpha2/leasecandidates | list or watch objects of kind LeaseCandidate |
| DELETE | /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates | delete collection of LeaseCandidate |
| GET | /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates | list or watch objects of kind LeaseCandidate |
| POST | /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates | create a LeaseCandidate |
| DELETE | /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name} | delete a LeaseCandidate |
| GET | /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name} | read the specified LeaseCandidate |
| PATCH | /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name} | partially update the specified LeaseCandidate |
| PUT | /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name} | replace the specified LeaseCandidate |
| GET | /apis/coordination.k8s.io/v1alpha2/watch/leasecandidates | watch individual changes to a list of LeaseCandidate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/coordination.k8s.io/v1alpha2/watch/namespaces/{namespace}/leasecandidates | watch individual changes to a list of LeaseCandidate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/coordination.k8s.io/v1alpha2/watch/namespaces/{namespace}/leasecandidates/{name} | watch changes to an object of kind LeaseCandidate. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/coordination.k8s.io/v1beta1/ | get available resources |
| GET | /apis/coordination.k8s.io/v1beta1/leasecandidates | list or watch objects of kind LeaseCandidate |
| DELETE | /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates | delete collection of LeaseCandidate |
| GET | /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates | list or watch objects of kind LeaseCandidate |
| POST | /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates | create a LeaseCandidate |
| DELETE | /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name} | delete a LeaseCandidate |
| GET | /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name} | read the specified LeaseCandidate |
| PATCH | /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name} | partially update the specified LeaseCandidate |
| PUT | /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name} | replace the specified LeaseCandidate |
| GET | /apis/coordination.k8s.io/v1beta1/watch/leasecandidates | watch individual changes to a list of LeaseCandidate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/coordination.k8s.io/v1beta1/watch/namespaces/{namespace}/leasecandidates | watch individual changes to a list of LeaseCandidate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/coordination.k8s.io/v1beta1/watch/namespaces/{namespace}/leasecandidates/{name} | watch changes to an object of kind LeaseCandidate. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/discovery.k8s.io/ | get information of a group |
| GET | /apis/discovery.k8s.io/v1/ | get available resources |
| GET | /apis/discovery.k8s.io/v1/endpointslices | list or watch objects of kind EndpointSlice |
| DELETE | /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices | delete collection of EndpointSlice |
| GET | /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices | list or watch objects of kind EndpointSlice |
| POST | /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices | create an EndpointSlice |
| DELETE | /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name} | delete an EndpointSlice |
| GET | /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name} | read the specified EndpointSlice |
| PATCH | /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name} | partially update the specified EndpointSlice |
| PUT | /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name} | replace the specified EndpointSlice |
| GET | /apis/discovery.k8s.io/v1/watch/endpointslices | watch individual changes to a list of EndpointSlice. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/discovery.k8s.io/v1/watch/namespaces/{namespace}/endpointslices | watch individual changes to a list of EndpointSlice. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/discovery.k8s.io/v1/watch/namespaces/{namespace}/endpointslices/{name} | watch changes to an object of kind EndpointSlice. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/events.k8s.io/ | get information of a group |
| GET | /apis/events.k8s.io/v1/ | get available resources |
| GET | /apis/events.k8s.io/v1/events | list or watch objects of kind Event |
| DELETE | /apis/events.k8s.io/v1/namespaces/{namespace}/events | delete collection of Event |
| GET | /apis/events.k8s.io/v1/namespaces/{namespace}/events | list or watch objects of kind Event |
| POST | /apis/events.k8s.io/v1/namespaces/{namespace}/events | create an Event |
| DELETE | /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name} | delete an Event |
| GET | /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name} | read the specified Event |
| PATCH | /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name} | partially update the specified Event |
| PUT | /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name} | replace the specified Event |
| GET | /apis/events.k8s.io/v1/watch/events | watch individual changes to a list of Event. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/events.k8s.io/v1/watch/namespaces/{namespace}/events | watch individual changes to a list of Event. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/events.k8s.io/v1/watch/namespaces/{namespace}/events/{name} | watch changes to an object of kind Event. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/flowcontrol.apiserver.k8s.io/ | get information of a group |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/ | get available resources |
| DELETE | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas | delete collection of FlowSchema |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas | list or watch objects of kind FlowSchema |
| POST | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas | create a FlowSchema |
| DELETE | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name} | delete a FlowSchema |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name} | read the specified FlowSchema |
| PATCH | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name} | partially update the specified FlowSchema |
| PUT | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name} | replace the specified FlowSchema |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}/status | read status of the specified FlowSchema |
| PATCH | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}/status | partially update status of the specified FlowSchema |
| PUT | /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}/status | replace status of the specified FlowSchema |
| DELETE | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations | delete collection of PriorityLevelConfiguration |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations | list or watch objects of kind PriorityLevelConfiguration |
| POST | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations | create a PriorityLevelConfiguration |
| DELETE | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name} | delete a PriorityLevelConfiguration |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name} | read the specified PriorityLevelConfiguration |
| PATCH | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name} | partially update the specified PriorityLevelConfiguration |
| PUT | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name} | replace the specified PriorityLevelConfiguration |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}/status | read status of the specified PriorityLevelConfiguration |
| PATCH | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}/status | partially update status of the specified PriorityLevelConfiguration |
| PUT | /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}/status | replace status of the specified PriorityLevelConfiguration |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/watch/flowschemas | watch individual changes to a list of FlowSchema. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/watch/flowschemas/{name} | watch changes to an object of kind FlowSchema. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/watch/prioritylevelconfigurations | watch individual changes to a list of PriorityLevelConfiguration. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/flowcontrol.apiserver.k8s.io/v1/watch/prioritylevelconfigurations/{name} | watch changes to an object of kind PriorityLevelConfiguration. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/internal.apiserver.k8s.io/ | get information of a group |
| GET | /apis/internal.apiserver.k8s.io/v1alpha1/ | get available resources |
| DELETE | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions | delete collection of StorageVersion |
| GET | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions | list or watch objects of kind StorageVersion |
| POST | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions | create a StorageVersion |
| DELETE | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name} | delete a StorageVersion |
| GET | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name} | read the specified StorageVersion |
| PATCH | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name} | partially update the specified StorageVersion |
| PUT | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name} | replace the specified StorageVersion |
| GET | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}/status | read status of the specified StorageVersion |
| PATCH | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}/status | partially update status of the specified StorageVersion |
| PUT | /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}/status | replace status of the specified StorageVersion |
| GET | /apis/internal.apiserver.k8s.io/v1alpha1/watch/storageversions | watch individual changes to a list of StorageVersion. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/internal.apiserver.k8s.io/v1alpha1/watch/storageversions/{name} | watch changes to an object of kind StorageVersion. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/networking.k8s.io/ | get information of a group |
| GET | /apis/networking.k8s.io/v1/ | get available resources |
| DELETE | /apis/networking.k8s.io/v1/ingressclasses | delete collection of IngressClass |
| GET | /apis/networking.k8s.io/v1/ingressclasses | list or watch objects of kind IngressClass |
| POST | /apis/networking.k8s.io/v1/ingressclasses | create an IngressClass |
| DELETE | /apis/networking.k8s.io/v1/ingressclasses/{name} | delete an IngressClass |
| GET | /apis/networking.k8s.io/v1/ingressclasses/{name} | read the specified IngressClass |
| PATCH | /apis/networking.k8s.io/v1/ingressclasses/{name} | partially update the specified IngressClass |
| PUT | /apis/networking.k8s.io/v1/ingressclasses/{name} | replace the specified IngressClass |
| GET | /apis/networking.k8s.io/v1/ingresses | list or watch objects of kind Ingress |
| DELETE | /apis/networking.k8s.io/v1/ipaddresses | delete collection of IPAddress |
| GET | /apis/networking.k8s.io/v1/ipaddresses | list or watch objects of kind IPAddress |
| POST | /apis/networking.k8s.io/v1/ipaddresses | create an IPAddress |
| DELETE | /apis/networking.k8s.io/v1/ipaddresses/{name} | delete an IPAddress |
| GET | /apis/networking.k8s.io/v1/ipaddresses/{name} | read the specified IPAddress |
| PATCH | /apis/networking.k8s.io/v1/ipaddresses/{name} | partially update the specified IPAddress |
| PUT | /apis/networking.k8s.io/v1/ipaddresses/{name} | replace the specified IPAddress |
| DELETE | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses | delete collection of Ingress |
| GET | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses | list or watch objects of kind Ingress |
| POST | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses | create an Ingress |
| DELETE | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name} | delete an Ingress |
| GET | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name} | read the specified Ingress |
| PATCH | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name} | partially update the specified Ingress |
| PUT | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name} | replace the specified Ingress |
| GET | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}/status | read status of the specified Ingress |
| PATCH | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}/status | partially update status of the specified Ingress |
| PUT | /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}/status | replace status of the specified Ingress |
| DELETE | /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies | delete collection of NetworkPolicy |
| GET | /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies | list or watch objects of kind NetworkPolicy |
| POST | /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies | create a NetworkPolicy |
| DELETE | /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name} | delete a NetworkPolicy |
| GET | /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name} | read the specified NetworkPolicy |
| PATCH | /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name} | partially update the specified NetworkPolicy |
| PUT | /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name} | replace the specified NetworkPolicy |
| GET | /apis/networking.k8s.io/v1/networkpolicies | list or watch objects of kind NetworkPolicy |
| DELETE | /apis/networking.k8s.io/v1/servicecidrs | delete collection of ServiceCIDR |
| GET | /apis/networking.k8s.io/v1/servicecidrs | list or watch objects of kind ServiceCIDR |
| POST | /apis/networking.k8s.io/v1/servicecidrs | create a ServiceCIDR |
| DELETE | /apis/networking.k8s.io/v1/servicecidrs/{name} | delete a ServiceCIDR |
| GET | /apis/networking.k8s.io/v1/servicecidrs/{name} | read the specified ServiceCIDR |
| PATCH | /apis/networking.k8s.io/v1/servicecidrs/{name} | partially update the specified ServiceCIDR |
| PUT | /apis/networking.k8s.io/v1/servicecidrs/{name} | replace the specified ServiceCIDR |
| GET | /apis/networking.k8s.io/v1/servicecidrs/{name}/status | read status of the specified ServiceCIDR |
| PATCH | /apis/networking.k8s.io/v1/servicecidrs/{name}/status | partially update status of the specified ServiceCIDR |
| PUT | /apis/networking.k8s.io/v1/servicecidrs/{name}/status | replace status of the specified ServiceCIDR |
| GET | /apis/networking.k8s.io/v1/watch/ingressclasses | watch individual changes to a list of IngressClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1/watch/ingressclasses/{name} | watch changes to an object of kind IngressClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/networking.k8s.io/v1/watch/ingresses | watch individual changes to a list of Ingress. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1/watch/ipaddresses | watch individual changes to a list of IPAddress. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1/watch/ipaddresses/{name} | watch changes to an object of kind IPAddress. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/ingresses | watch individual changes to a list of Ingress. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/ingresses/{name} | watch changes to an object of kind Ingress. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/networkpolicies | watch individual changes to a list of NetworkPolicy. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/networkpolicies/{name} | watch changes to an object of kind NetworkPolicy. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/networking.k8s.io/v1/watch/networkpolicies | watch individual changes to a list of NetworkPolicy. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1/watch/servicecidrs | watch individual changes to a list of ServiceCIDR. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1/watch/servicecidrs/{name} | watch changes to an object of kind ServiceCIDR. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/networking.k8s.io/v1beta1/ | get available resources |
| DELETE | /apis/networking.k8s.io/v1beta1/ipaddresses | delete collection of IPAddress |
| GET | /apis/networking.k8s.io/v1beta1/ipaddresses | list or watch objects of kind IPAddress |
| POST | /apis/networking.k8s.io/v1beta1/ipaddresses | create an IPAddress |
| DELETE | /apis/networking.k8s.io/v1beta1/ipaddresses/{name} | delete an IPAddress |
| GET | /apis/networking.k8s.io/v1beta1/ipaddresses/{name} | read the specified IPAddress |
| PATCH | /apis/networking.k8s.io/v1beta1/ipaddresses/{name} | partially update the specified IPAddress |
| PUT | /apis/networking.k8s.io/v1beta1/ipaddresses/{name} | replace the specified IPAddress |
| DELETE | /apis/networking.k8s.io/v1beta1/servicecidrs | delete collection of ServiceCIDR |
| GET | /apis/networking.k8s.io/v1beta1/servicecidrs | list or watch objects of kind ServiceCIDR |
| POST | /apis/networking.k8s.io/v1beta1/servicecidrs | create a ServiceCIDR |
| DELETE | /apis/networking.k8s.io/v1beta1/servicecidrs/{name} | delete a ServiceCIDR |
| GET | /apis/networking.k8s.io/v1beta1/servicecidrs/{name} | read the specified ServiceCIDR |
| PATCH | /apis/networking.k8s.io/v1beta1/servicecidrs/{name} | partially update the specified ServiceCIDR |
| PUT | /apis/networking.k8s.io/v1beta1/servicecidrs/{name} | replace the specified ServiceCIDR |
| GET | /apis/networking.k8s.io/v1beta1/servicecidrs/{name}/status | read status of the specified ServiceCIDR |
| PATCH | /apis/networking.k8s.io/v1beta1/servicecidrs/{name}/status | partially update status of the specified ServiceCIDR |
| PUT | /apis/networking.k8s.io/v1beta1/servicecidrs/{name}/status | replace status of the specified ServiceCIDR |
| GET | /apis/networking.k8s.io/v1beta1/watch/ipaddresses | watch individual changes to a list of IPAddress. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1beta1/watch/ipaddresses/{name} | watch changes to an object of kind IPAddress. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/networking.k8s.io/v1beta1/watch/servicecidrs | watch individual changes to a list of ServiceCIDR. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/networking.k8s.io/v1beta1/watch/servicecidrs/{name} | watch changes to an object of kind ServiceCIDR. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/node.k8s.io/ | get information of a group |
| GET | /apis/node.k8s.io/v1/ | get available resources |
| DELETE | /apis/node.k8s.io/v1/runtimeclasses | delete collection of RuntimeClass |
| GET | /apis/node.k8s.io/v1/runtimeclasses | list or watch objects of kind RuntimeClass |
| POST | /apis/node.k8s.io/v1/runtimeclasses | create a RuntimeClass |
| DELETE | /apis/node.k8s.io/v1/runtimeclasses/{name} | delete a RuntimeClass |
| GET | /apis/node.k8s.io/v1/runtimeclasses/{name} | read the specified RuntimeClass |
| PATCH | /apis/node.k8s.io/v1/runtimeclasses/{name} | partially update the specified RuntimeClass |
| PUT | /apis/node.k8s.io/v1/runtimeclasses/{name} | replace the specified RuntimeClass |
| GET | /apis/node.k8s.io/v1/watch/runtimeclasses | watch individual changes to a list of RuntimeClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/node.k8s.io/v1/watch/runtimeclasses/{name} | watch changes to an object of kind RuntimeClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/policy/ | get information of a group |
| GET | /apis/policy/v1/ | get available resources |
| DELETE | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets | delete collection of PodDisruptionBudget |
| GET | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets | list or watch objects of kind PodDisruptionBudget |
| POST | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets | create a PodDisruptionBudget |
| DELETE | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name} | delete a PodDisruptionBudget |
| GET | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name} | read the specified PodDisruptionBudget |
| PATCH | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name} | partially update the specified PodDisruptionBudget |
| PUT | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name} | replace the specified PodDisruptionBudget |
| GET | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}/status | read status of the specified PodDisruptionBudget |
| PATCH | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}/status | partially update status of the specified PodDisruptionBudget |
| PUT | /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}/status | replace status of the specified PodDisruptionBudget |
| GET | /apis/policy/v1/poddisruptionbudgets | list or watch objects of kind PodDisruptionBudget |
| GET | /apis/policy/v1/watch/namespaces/{namespace}/poddisruptionbudgets | watch individual changes to a list of PodDisruptionBudget. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/policy/v1/watch/namespaces/{namespace}/poddisruptionbudgets/{name} | watch changes to an object of kind PodDisruptionBudget. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/policy/v1/watch/poddisruptionbudgets | watch individual changes to a list of PodDisruptionBudget. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/rbac.authorization.k8s.io/ | get information of a group |
| GET | /apis/rbac.authorization.k8s.io/v1/ | get available resources |
| DELETE | /apis/rbac.authorization.k8s.io/v1/clusterrolebindings | delete collection of ClusterRoleBinding |
| GET | /apis/rbac.authorization.k8s.io/v1/clusterrolebindings | list or watch objects of kind ClusterRoleBinding |
| POST | /apis/rbac.authorization.k8s.io/v1/clusterrolebindings | create a ClusterRoleBinding |
| DELETE | /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name} | delete a ClusterRoleBinding |
| GET | /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name} | read the specified ClusterRoleBinding |
| PATCH | /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name} | partially update the specified ClusterRoleBinding |
| PUT | /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name} | replace the specified ClusterRoleBinding |
| DELETE | /apis/rbac.authorization.k8s.io/v1/clusterroles | delete collection of ClusterRole |
| GET | /apis/rbac.authorization.k8s.io/v1/clusterroles | list or watch objects of kind ClusterRole |
| POST | /apis/rbac.authorization.k8s.io/v1/clusterroles | create a ClusterRole |
| DELETE | /apis/rbac.authorization.k8s.io/v1/clusterroles/{name} | delete a ClusterRole |
| GET | /apis/rbac.authorization.k8s.io/v1/clusterroles/{name} | read the specified ClusterRole |
| PATCH | /apis/rbac.authorization.k8s.io/v1/clusterroles/{name} | partially update the specified ClusterRole |
| PUT | /apis/rbac.authorization.k8s.io/v1/clusterroles/{name} | replace the specified ClusterRole |
| DELETE | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings | delete collection of RoleBinding |
| GET | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings | list or watch objects of kind RoleBinding |
| POST | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings | create a RoleBinding |
| DELETE | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name} | delete a RoleBinding |
| GET | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name} | read the specified RoleBinding |
| PATCH | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name} | partially update the specified RoleBinding |
| PUT | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name} | replace the specified RoleBinding |
| DELETE | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles | delete collection of Role |
| GET | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles | list or watch objects of kind Role |
| POST | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles | create a Role |
| DELETE | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name} | delete a Role |
| GET | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name} | read the specified Role |
| PATCH | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name} | partially update the specified Role |
| PUT | /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name} | replace the specified Role |
| GET | /apis/rbac.authorization.k8s.io/v1/rolebindings | list or watch objects of kind RoleBinding |
| GET | /apis/rbac.authorization.k8s.io/v1/roles | list or watch objects of kind Role |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/clusterrolebindings | watch individual changes to a list of ClusterRoleBinding. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/clusterrolebindings/{name} | watch changes to an object of kind ClusterRoleBinding. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/clusterroles | watch individual changes to a list of ClusterRole. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/clusterroles/{name} | watch changes to an object of kind ClusterRole. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/rolebindings | watch individual changes to a list of RoleBinding. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/rolebindings/{name} | watch changes to an object of kind RoleBinding. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/roles | watch individual changes to a list of Role. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/roles/{name} | watch changes to an object of kind Role. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/rolebindings | watch individual changes to a list of RoleBinding. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/rbac.authorization.k8s.io/v1/watch/roles | watch individual changes to a list of Role. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/ | get information of a group |
| GET | /apis/resource.k8s.io/v1/ | get available resources |
| DELETE | /apis/resource.k8s.io/v1/deviceclasses | delete collection of DeviceClass |
| GET | /apis/resource.k8s.io/v1/deviceclasses | list or watch objects of kind DeviceClass |
| POST | /apis/resource.k8s.io/v1/deviceclasses | create a DeviceClass |
| DELETE | /apis/resource.k8s.io/v1/deviceclasses/{name} | delete a DeviceClass |
| GET | /apis/resource.k8s.io/v1/deviceclasses/{name} | read the specified DeviceClass |
| PATCH | /apis/resource.k8s.io/v1/deviceclasses/{name} | partially update the specified DeviceClass |
| PUT | /apis/resource.k8s.io/v1/deviceclasses/{name} | replace the specified DeviceClass |
| DELETE | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims | delete collection of ResourceClaim |
| GET | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims | list or watch objects of kind ResourceClaim |
| POST | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims | create a ResourceClaim |
| DELETE | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name} | delete a ResourceClaim |
| GET | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name} | read the specified ResourceClaim |
| PATCH | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name} | partially update the specified ResourceClaim |
| PUT | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name} | replace the specified ResourceClaim |
| GET | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}/status | read status of the specified ResourceClaim |
| PATCH | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}/status | partially update status of the specified ResourceClaim |
| PUT | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}/status | replace status of the specified ResourceClaim |
| DELETE | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates | delete collection of ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates | list or watch objects of kind ResourceClaimTemplate |
| POST | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates | create a ResourceClaimTemplate |
| DELETE | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name} | delete a ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name} | read the specified ResourceClaimTemplate |
| PATCH | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name} | partially update the specified ResourceClaimTemplate |
| PUT | /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name} | replace the specified ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1/resourceclaims | list or watch objects of kind ResourceClaim |
| GET | /apis/resource.k8s.io/v1/resourceclaimtemplates | list or watch objects of kind ResourceClaimTemplate |
| DELETE | /apis/resource.k8s.io/v1/resourceslices | delete collection of ResourceSlice |
| GET | /apis/resource.k8s.io/v1/resourceslices | list or watch objects of kind ResourceSlice |
| POST | /apis/resource.k8s.io/v1/resourceslices | create a ResourceSlice |
| DELETE | /apis/resource.k8s.io/v1/resourceslices/{name} | delete a ResourceSlice |
| GET | /apis/resource.k8s.io/v1/resourceslices/{name} | read the specified ResourceSlice |
| PATCH | /apis/resource.k8s.io/v1/resourceslices/{name} | partially update the specified ResourceSlice |
| PUT | /apis/resource.k8s.io/v1/resourceslices/{name} | replace the specified ResourceSlice |
| GET | /apis/resource.k8s.io/v1/watch/deviceclasses | watch individual changes to a list of DeviceClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1/watch/deviceclasses/{name} | watch changes to an object of kind DeviceClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaims | watch individual changes to a list of ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaims/{name} | watch changes to an object of kind ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaimtemplates | watch individual changes to a list of ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaimtemplates/{name} | watch changes to an object of kind ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1/watch/resourceclaims | watch individual changes to a list of ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1/watch/resourceclaimtemplates | watch individual changes to a list of ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1/watch/resourceslices | watch individual changes to a list of ResourceSlice. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1/watch/resourceslices/{name} | watch changes to an object of kind ResourceSlice. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1alpha3/ | get available resources |
| DELETE | /apis/resource.k8s.io/v1alpha3/devicetaintrules | delete collection of DeviceTaintRule |
| GET | /apis/resource.k8s.io/v1alpha3/devicetaintrules | list or watch objects of kind DeviceTaintRule |
| POST | /apis/resource.k8s.io/v1alpha3/devicetaintrules | create a DeviceTaintRule |
| DELETE | /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name} | delete a DeviceTaintRule |
| GET | /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name} | read the specified DeviceTaintRule |
| PATCH | /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name} | partially update the specified DeviceTaintRule |
| PUT | /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name} | replace the specified DeviceTaintRule |
| GET | /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}/status | read status of the specified DeviceTaintRule |
| PATCH | /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}/status | partially update status of the specified DeviceTaintRule |
| PUT | /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}/status | replace status of the specified DeviceTaintRule |
| GET | /apis/resource.k8s.io/v1alpha3/watch/devicetaintrules | watch individual changes to a list of DeviceTaintRule. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1alpha3/watch/devicetaintrules/{name} | watch changes to an object of kind DeviceTaintRule. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta1/ | get available resources |
| DELETE | /apis/resource.k8s.io/v1beta1/deviceclasses | delete collection of DeviceClass |
| GET | /apis/resource.k8s.io/v1beta1/deviceclasses | list or watch objects of kind DeviceClass |
| POST | /apis/resource.k8s.io/v1beta1/deviceclasses | create a DeviceClass |
| DELETE | /apis/resource.k8s.io/v1beta1/deviceclasses/{name} | delete a DeviceClass |
| GET | /apis/resource.k8s.io/v1beta1/deviceclasses/{name} | read the specified DeviceClass |
| PATCH | /apis/resource.k8s.io/v1beta1/deviceclasses/{name} | partially update the specified DeviceClass |
| PUT | /apis/resource.k8s.io/v1beta1/deviceclasses/{name} | replace the specified DeviceClass |
| DELETE | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims | delete collection of ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims | list or watch objects of kind ResourceClaim |
| POST | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims | create a ResourceClaim |
| DELETE | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name} | delete a ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name} | read the specified ResourceClaim |
| PATCH | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name} | partially update the specified ResourceClaim |
| PUT | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name} | replace the specified ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}/status | read status of the specified ResourceClaim |
| PATCH | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}/status | partially update status of the specified ResourceClaim |
| PUT | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}/status | replace status of the specified ResourceClaim |
| DELETE | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates | delete collection of ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates | list or watch objects of kind ResourceClaimTemplate |
| POST | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates | create a ResourceClaimTemplate |
| DELETE | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name} | delete a ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name} | read the specified ResourceClaimTemplate |
| PATCH | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name} | partially update the specified ResourceClaimTemplate |
| PUT | /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name} | replace the specified ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1beta1/resourceclaims | list or watch objects of kind ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta1/resourceclaimtemplates | list or watch objects of kind ResourceClaimTemplate |
| DELETE | /apis/resource.k8s.io/v1beta1/resourceslices | delete collection of ResourceSlice |
| GET | /apis/resource.k8s.io/v1beta1/resourceslices | list or watch objects of kind ResourceSlice |
| POST | /apis/resource.k8s.io/v1beta1/resourceslices | create a ResourceSlice |
| DELETE | /apis/resource.k8s.io/v1beta1/resourceslices/{name} | delete a ResourceSlice |
| GET | /apis/resource.k8s.io/v1beta1/resourceslices/{name} | read the specified ResourceSlice |
| PATCH | /apis/resource.k8s.io/v1beta1/resourceslices/{name} | partially update the specified ResourceSlice |
| PUT | /apis/resource.k8s.io/v1beta1/resourceslices/{name} | replace the specified ResourceSlice |
| GET | /apis/resource.k8s.io/v1beta1/watch/deviceclasses | watch individual changes to a list of DeviceClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta1/watch/deviceclasses/{name} | watch changes to an object of kind DeviceClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaims | watch individual changes to a list of ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaims/{name} | watch changes to an object of kind ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaimtemplates | watch individual changes to a list of ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaimtemplates/{name} | watch changes to an object of kind ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta1/watch/resourceclaims | watch individual changes to a list of ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta1/watch/resourceclaimtemplates | watch individual changes to a list of ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta1/watch/resourceslices | watch individual changes to a list of ResourceSlice. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta1/watch/resourceslices/{name} | watch changes to an object of kind ResourceSlice. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta2/ | get available resources |
| DELETE | /apis/resource.k8s.io/v1beta2/deviceclasses | delete collection of DeviceClass |
| GET | /apis/resource.k8s.io/v1beta2/deviceclasses | list or watch objects of kind DeviceClass |
| POST | /apis/resource.k8s.io/v1beta2/deviceclasses | create a DeviceClass |
| DELETE | /apis/resource.k8s.io/v1beta2/deviceclasses/{name} | delete a DeviceClass |
| GET | /apis/resource.k8s.io/v1beta2/deviceclasses/{name} | read the specified DeviceClass |
| PATCH | /apis/resource.k8s.io/v1beta2/deviceclasses/{name} | partially update the specified DeviceClass |
| PUT | /apis/resource.k8s.io/v1beta2/deviceclasses/{name} | replace the specified DeviceClass |
| DELETE | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims | delete collection of ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims | list or watch objects of kind ResourceClaim |
| POST | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims | create a ResourceClaim |
| DELETE | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name} | delete a ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name} | read the specified ResourceClaim |
| PATCH | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name} | partially update the specified ResourceClaim |
| PUT | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name} | replace the specified ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}/status | read status of the specified ResourceClaim |
| PATCH | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}/status | partially update status of the specified ResourceClaim |
| PUT | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}/status | replace status of the specified ResourceClaim |
| DELETE | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates | delete collection of ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates | list or watch objects of kind ResourceClaimTemplate |
| POST | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates | create a ResourceClaimTemplate |
| DELETE | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name} | delete a ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name} | read the specified ResourceClaimTemplate |
| PATCH | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name} | partially update the specified ResourceClaimTemplate |
| PUT | /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name} | replace the specified ResourceClaimTemplate |
| GET | /apis/resource.k8s.io/v1beta2/resourceclaims | list or watch objects of kind ResourceClaim |
| GET | /apis/resource.k8s.io/v1beta2/resourceclaimtemplates | list or watch objects of kind ResourceClaimTemplate |
| DELETE | /apis/resource.k8s.io/v1beta2/resourceslices | delete collection of ResourceSlice |
| GET | /apis/resource.k8s.io/v1beta2/resourceslices | list or watch objects of kind ResourceSlice |
| POST | /apis/resource.k8s.io/v1beta2/resourceslices | create a ResourceSlice |
| DELETE | /apis/resource.k8s.io/v1beta2/resourceslices/{name} | delete a ResourceSlice |
| GET | /apis/resource.k8s.io/v1beta2/resourceslices/{name} | read the specified ResourceSlice |
| PATCH | /apis/resource.k8s.io/v1beta2/resourceslices/{name} | partially update the specified ResourceSlice |
| PUT | /apis/resource.k8s.io/v1beta2/resourceslices/{name} | replace the specified ResourceSlice |
| GET | /apis/resource.k8s.io/v1beta2/watch/deviceclasses | watch individual changes to a list of DeviceClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta2/watch/deviceclasses/{name} | watch changes to an object of kind DeviceClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaims | watch individual changes to a list of ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaims/{name} | watch changes to an object of kind ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaimtemplates | watch individual changes to a list of ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaimtemplates/{name} | watch changes to an object of kind ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/resource.k8s.io/v1beta2/watch/resourceclaims | watch individual changes to a list of ResourceClaim. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta2/watch/resourceclaimtemplates | watch individual changes to a list of ResourceClaimTemplate. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta2/watch/resourceslices | watch individual changes to a list of ResourceSlice. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/resource.k8s.io/v1beta2/watch/resourceslices/{name} | watch changes to an object of kind ResourceSlice. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/scheduling.k8s.io/ | get information of a group |
| GET | /apis/scheduling.k8s.io/v1/ | get available resources |
| DELETE | /apis/scheduling.k8s.io/v1/priorityclasses | delete collection of PriorityClass |
| GET | /apis/scheduling.k8s.io/v1/priorityclasses | list or watch objects of kind PriorityClass |
| POST | /apis/scheduling.k8s.io/v1/priorityclasses | create a PriorityClass |
| DELETE | /apis/scheduling.k8s.io/v1/priorityclasses/{name} | delete a PriorityClass |
| GET | /apis/scheduling.k8s.io/v1/priorityclasses/{name} | read the specified PriorityClass |
| PATCH | /apis/scheduling.k8s.io/v1/priorityclasses/{name} | partially update the specified PriorityClass |
| PUT | /apis/scheduling.k8s.io/v1/priorityclasses/{name} | replace the specified PriorityClass |
| GET | /apis/scheduling.k8s.io/v1/watch/priorityclasses | watch individual changes to a list of PriorityClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/scheduling.k8s.io/v1/watch/priorityclasses/{name} | watch changes to an object of kind PriorityClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/scheduling.k8s.io/v1alpha1/ | get available resources |
| DELETE | /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads | delete collection of Workload |
| GET | /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads | list or watch objects of kind Workload |
| POST | /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads | create a Workload |
| DELETE | /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name} | delete a Workload |
| GET | /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name} | read the specified Workload |
| PATCH | /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name} | partially update the specified Workload |
| PUT | /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name} | replace the specified Workload |
| GET | /apis/scheduling.k8s.io/v1alpha1/watch/namespaces/{namespace}/workloads | watch individual changes to a list of Workload. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/scheduling.k8s.io/v1alpha1/watch/namespaces/{namespace}/workloads/{name} | watch changes to an object of kind Workload. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/scheduling.k8s.io/v1alpha1/watch/workloads | watch individual changes to a list of Workload. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/scheduling.k8s.io/v1alpha1/workloads | list or watch objects of kind Workload |
| GET | /apis/storage.k8s.io/ | get information of a group |
| GET | /apis/storage.k8s.io/v1/ | get available resources |
| DELETE | /apis/storage.k8s.io/v1/csidrivers | delete collection of CSIDriver |
| GET | /apis/storage.k8s.io/v1/csidrivers | list or watch objects of kind CSIDriver |
| POST | /apis/storage.k8s.io/v1/csidrivers | create a CSIDriver |
| DELETE | /apis/storage.k8s.io/v1/csidrivers/{name} | delete a CSIDriver |
| GET | /apis/storage.k8s.io/v1/csidrivers/{name} | read the specified CSIDriver |
| PATCH | /apis/storage.k8s.io/v1/csidrivers/{name} | partially update the specified CSIDriver |
| PUT | /apis/storage.k8s.io/v1/csidrivers/{name} | replace the specified CSIDriver |
| DELETE | /apis/storage.k8s.io/v1/csinodes | delete collection of CSINode |
| GET | /apis/storage.k8s.io/v1/csinodes | list or watch objects of kind CSINode |
| POST | /apis/storage.k8s.io/v1/csinodes | create a CSINode |
| DELETE | /apis/storage.k8s.io/v1/csinodes/{name} | delete a CSINode |
| GET | /apis/storage.k8s.io/v1/csinodes/{name} | read the specified CSINode |
| PATCH | /apis/storage.k8s.io/v1/csinodes/{name} | partially update the specified CSINode |
| PUT | /apis/storage.k8s.io/v1/csinodes/{name} | replace the specified CSINode |
| GET | /apis/storage.k8s.io/v1/csistoragecapacities | list or watch objects of kind CSIStorageCapacity |
| DELETE | /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities | delete collection of CSIStorageCapacity |
| GET | /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities | list or watch objects of kind CSIStorageCapacity |
| POST | /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities | create a CSIStorageCapacity |
| DELETE | /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name} | delete a CSIStorageCapacity |
| GET | /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name} | read the specified CSIStorageCapacity |
| PATCH | /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name} | partially update the specified CSIStorageCapacity |
| PUT | /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name} | replace the specified CSIStorageCapacity |
| DELETE | /apis/storage.k8s.io/v1/storageclasses | delete collection of StorageClass |
| GET | /apis/storage.k8s.io/v1/storageclasses | list or watch objects of kind StorageClass |
| POST | /apis/storage.k8s.io/v1/storageclasses | create a StorageClass |
| DELETE | /apis/storage.k8s.io/v1/storageclasses/{name} | delete a StorageClass |
| GET | /apis/storage.k8s.io/v1/storageclasses/{name} | read the specified StorageClass |
| PATCH | /apis/storage.k8s.io/v1/storageclasses/{name} | partially update the specified StorageClass |
| PUT | /apis/storage.k8s.io/v1/storageclasses/{name} | replace the specified StorageClass |
| DELETE | /apis/storage.k8s.io/v1/volumeattachments | delete collection of VolumeAttachment |
| GET | /apis/storage.k8s.io/v1/volumeattachments | list or watch objects of kind VolumeAttachment |
| POST | /apis/storage.k8s.io/v1/volumeattachments | create a VolumeAttachment |
| DELETE | /apis/storage.k8s.io/v1/volumeattachments/{name} | delete a VolumeAttachment |
| GET | /apis/storage.k8s.io/v1/volumeattachments/{name} | read the specified VolumeAttachment |
| PATCH | /apis/storage.k8s.io/v1/volumeattachments/{name} | partially update the specified VolumeAttachment |
| PUT | /apis/storage.k8s.io/v1/volumeattachments/{name} | replace the specified VolumeAttachment |
| GET | /apis/storage.k8s.io/v1/volumeattachments/{name}/status | read status of the specified VolumeAttachment |
| PATCH | /apis/storage.k8s.io/v1/volumeattachments/{name}/status | partially update status of the specified VolumeAttachment |
| PUT | /apis/storage.k8s.io/v1/volumeattachments/{name}/status | replace status of the specified VolumeAttachment |
| DELETE | /apis/storage.k8s.io/v1/volumeattributesclasses | delete collection of VolumeAttributesClass |
| GET | /apis/storage.k8s.io/v1/volumeattributesclasses | list or watch objects of kind VolumeAttributesClass |
| POST | /apis/storage.k8s.io/v1/volumeattributesclasses | create a VolumeAttributesClass |
| DELETE | /apis/storage.k8s.io/v1/volumeattributesclasses/{name} | delete a VolumeAttributesClass |
| GET | /apis/storage.k8s.io/v1/volumeattributesclasses/{name} | read the specified VolumeAttributesClass |
| PATCH | /apis/storage.k8s.io/v1/volumeattributesclasses/{name} | partially update the specified VolumeAttributesClass |
| PUT | /apis/storage.k8s.io/v1/volumeattributesclasses/{name} | replace the specified VolumeAttributesClass |
| GET | /apis/storage.k8s.io/v1/watch/csidrivers | watch individual changes to a list of CSIDriver. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1/watch/csidrivers/{name} | watch changes to an object of kind CSIDriver. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/storage.k8s.io/v1/watch/csinodes | watch individual changes to a list of CSINode. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1/watch/csinodes/{name} | watch changes to an object of kind CSINode. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/storage.k8s.io/v1/watch/csistoragecapacities | watch individual changes to a list of CSIStorageCapacity. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1/watch/namespaces/{namespace}/csistoragecapacities | watch individual changes to a list of CSIStorageCapacity. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1/watch/namespaces/{namespace}/csistoragecapacities/{name} | watch changes to an object of kind CSIStorageCapacity. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/storage.k8s.io/v1/watch/storageclasses | watch individual changes to a list of StorageClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1/watch/storageclasses/{name} | watch changes to an object of kind StorageClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/storage.k8s.io/v1/watch/volumeattachments | watch individual changes to a list of VolumeAttachment. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1/watch/volumeattachments/{name} | watch changes to an object of kind VolumeAttachment. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/storage.k8s.io/v1/watch/volumeattributesclasses | watch individual changes to a list of VolumeAttributesClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1/watch/volumeattributesclasses/{name} | watch changes to an object of kind VolumeAttributesClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/storage.k8s.io/v1beta1/ | get available resources |
| DELETE | /apis/storage.k8s.io/v1beta1/volumeattributesclasses | delete collection of VolumeAttributesClass |
| GET | /apis/storage.k8s.io/v1beta1/volumeattributesclasses | list or watch objects of kind VolumeAttributesClass |
| POST | /apis/storage.k8s.io/v1beta1/volumeattributesclasses | create a VolumeAttributesClass |
| DELETE | /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name} | delete a VolumeAttributesClass |
| GET | /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name} | read the specified VolumeAttributesClass |
| PATCH | /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name} | partially update the specified VolumeAttributesClass |
| PUT | /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name} | replace the specified VolumeAttributesClass |
| GET | /apis/storage.k8s.io/v1beta1/watch/volumeattributesclasses | watch individual changes to a list of VolumeAttributesClass. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storage.k8s.io/v1beta1/watch/volumeattributesclasses/{name} | watch changes to an object of kind VolumeAttributesClass. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |
| GET | /apis/storagemigration.k8s.io/ | get information of a group |
| GET | /apis/storagemigration.k8s.io/v1beta1/ | get available resources |
| DELETE | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations | delete collection of StorageVersionMigration |
| GET | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations | list or watch objects of kind StorageVersionMigration |
| POST | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations | create a StorageVersionMigration |
| DELETE | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name} | delete a StorageVersionMigration |
| GET | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name} | read the specified StorageVersionMigration |
| PATCH | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name} | partially update the specified StorageVersionMigration |
| PUT | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name} | replace the specified StorageVersionMigration |
| GET | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}/status | read status of the specified StorageVersionMigration |
| PATCH | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}/status | partially update status of the specified StorageVersionMigration |
| PUT | /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}/status | replace status of the specified StorageVersionMigration |
| GET | /apis/storagemigration.k8s.io/v1beta1/watch/storageversionmigrations | watch individual changes to a list of StorageVersionMigration. deprecated: use the 'watch' parameter with a list operation instead. |
| GET | /apis/storagemigration.k8s.io/v1beta1/watch/storageversionmigrations/{name} | watch changes to an object of kind StorageVersionMigration. deprecated: use the 'watch' parameter with a list operation instead, filtered to a single item with the 'fieldSelector' parameter. |

### logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /logs/ |  |
| GET | /logs/{logpath} |  |

### openid
| Method | Path | Description |
|--------|------|-------------|
| GET | /openid/v1/jwks/ | get service account issuer OpenID JSON Web Key Set (contains public token verification keys) |

### version
| Method | Path | Description |
|--------|------|-------------|
| GET | /version/ | get the version information for this server |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all openid-configuration?" -> GET /.well-known/openid-configuration/
- "List all api?" -> GET /api/
- "List all api?" -> GET /api/v1/
- "List all componentstatuses?" -> GET /api/v1/componentstatuses
- "Get componentstatuse details?" -> GET /api/v1/componentstatuses/{name}
- "List all configmaps?" -> GET /api/v1/configmaps
- "List all endpoints?" -> GET /api/v1/endpoints
- "List all events?" -> GET /api/v1/events
- "List all limitranges?" -> GET /api/v1/limitranges
- "List all namespaces?" -> GET /api/v1/namespaces
- "Create a namespace?" -> POST /api/v1/namespaces
- "Create a binding?" -> POST /api/v1/namespaces/{namespace}/bindings
- "List all configmaps?" -> GET /api/v1/namespaces/{namespace}/configmaps
- "Create a configmap?" -> POST /api/v1/namespaces/{namespace}/configmaps
- "Delete a configmap?" -> DELETE /api/v1/namespaces/{namespace}/configmaps/{name}
- "Get configmap details?" -> GET /api/v1/namespaces/{namespace}/configmaps/{name}
- "Partially update a configmap?" -> PATCH /api/v1/namespaces/{namespace}/configmaps/{name}
- "Update a configmap?" -> PUT /api/v1/namespaces/{namespace}/configmaps/{name}
- "List all endpoints?" -> GET /api/v1/namespaces/{namespace}/endpoints
- "Create a endpoint?" -> POST /api/v1/namespaces/{namespace}/endpoints
- "Delete a endpoint?" -> DELETE /api/v1/namespaces/{namespace}/endpoints/{name}
- "Get endpoint details?" -> GET /api/v1/namespaces/{namespace}/endpoints/{name}
- "Partially update a endpoint?" -> PATCH /api/v1/namespaces/{namespace}/endpoints/{name}
- "Update a endpoint?" -> PUT /api/v1/namespaces/{namespace}/endpoints/{name}
- "List all events?" -> GET /api/v1/namespaces/{namespace}/events
- "Create a event?" -> POST /api/v1/namespaces/{namespace}/events
- "Delete a event?" -> DELETE /api/v1/namespaces/{namespace}/events/{name}
- "Get event details?" -> GET /api/v1/namespaces/{namespace}/events/{name}
- "Partially update a event?" -> PATCH /api/v1/namespaces/{namespace}/events/{name}
- "Update a event?" -> PUT /api/v1/namespaces/{namespace}/events/{name}
- "List all limitranges?" -> GET /api/v1/namespaces/{namespace}/limitranges
- "Create a limitrange?" -> POST /api/v1/namespaces/{namespace}/limitranges
- "Delete a limitrange?" -> DELETE /api/v1/namespaces/{namespace}/limitranges/{name}
- "Get limitrange details?" -> GET /api/v1/namespaces/{namespace}/limitranges/{name}
- "Partially update a limitrange?" -> PATCH /api/v1/namespaces/{namespace}/limitranges/{name}
- "Update a limitrange?" -> PUT /api/v1/namespaces/{namespace}/limitranges/{name}
- "List all persistentvolumeclaims?" -> GET /api/v1/namespaces/{namespace}/persistentvolumeclaims
- "Create a persistentvolumeclaim?" -> POST /api/v1/namespaces/{namespace}/persistentvolumeclaims
- "Delete a persistentvolumeclaim?" -> DELETE /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}
- "Get persistentvolumeclaim details?" -> GET /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}
- "Partially update a persistentvolumeclaim?" -> PATCH /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}
- "Update a persistentvolumeclaim?" -> PUT /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}
- "List all status?" -> GET /api/v1/namespaces/{namespace}/persistentvolumeclaims/{name}/status
- "List all pods?" -> GET /api/v1/namespaces/{namespace}/pods
- "Create a pod?" -> POST /api/v1/namespaces/{namespace}/pods
- "Delete a pod?" -> DELETE /api/v1/namespaces/{namespace}/pods/{name}
- "Get pod details?" -> GET /api/v1/namespaces/{namespace}/pods/{name}
- "Partially update a pod?" -> PATCH /api/v1/namespaces/{namespace}/pods/{name}
- "Update a pod?" -> PUT /api/v1/namespaces/{namespace}/pods/{name}
- "List all attach?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/attach
- "Create a attach?" -> POST /api/v1/namespaces/{namespace}/pods/{name}/attach
- "Create a binding?" -> POST /api/v1/namespaces/{namespace}/pods/{name}/binding
- "List all ephemeralcontainers?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/ephemeralcontainers
- "Create a eviction?" -> POST /api/v1/namespaces/{namespace}/pods/{name}/eviction
- "List all exec?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/exec
- "Create a exec?" -> POST /api/v1/namespaces/{namespace}/pods/{name}/exec
- "List all log?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/log
- "List all portforward?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/portforward
- "Create a portforward?" -> POST /api/v1/namespaces/{namespace}/pods/{name}/portforward
- "List all proxy?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/proxy
- "Create a proxy?" -> POST /api/v1/namespaces/{namespace}/pods/{name}/proxy
- "Delete a proxy?" -> DELETE /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path}
- "Get proxy details?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path}
- "Partially update a proxy?" -> PATCH /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path}
- "Update a proxy?" -> PUT /api/v1/namespaces/{namespace}/pods/{name}/proxy/{path}
- "List all resize?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/resize
- "List all status?" -> GET /api/v1/namespaces/{namespace}/pods/{name}/status
- "List all podtemplates?" -> GET /api/v1/namespaces/{namespace}/podtemplates
- "Create a podtemplate?" -> POST /api/v1/namespaces/{namespace}/podtemplates
- "Delete a podtemplate?" -> DELETE /api/v1/namespaces/{namespace}/podtemplates/{name}
- "Get podtemplate details?" -> GET /api/v1/namespaces/{namespace}/podtemplates/{name}
- "Partially update a podtemplate?" -> PATCH /api/v1/namespaces/{namespace}/podtemplates/{name}
- "Update a podtemplate?" -> PUT /api/v1/namespaces/{namespace}/podtemplates/{name}
- "List all replicationcontrollers?" -> GET /api/v1/namespaces/{namespace}/replicationcontrollers
- "Create a replicationcontroller?" -> POST /api/v1/namespaces/{namespace}/replicationcontrollers
- "Delete a replicationcontroller?" -> DELETE /api/v1/namespaces/{namespace}/replicationcontrollers/{name}
- "Get replicationcontroller details?" -> GET /api/v1/namespaces/{namespace}/replicationcontrollers/{name}
- "Partially update a replicationcontroller?" -> PATCH /api/v1/namespaces/{namespace}/replicationcontrollers/{name}
- "Update a replicationcontroller?" -> PUT /api/v1/namespaces/{namespace}/replicationcontrollers/{name}
- "List all scale?" -> GET /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/scale
- "List all status?" -> GET /api/v1/namespaces/{namespace}/replicationcontrollers/{name}/status
- "List all resourcequotas?" -> GET /api/v1/namespaces/{namespace}/resourcequotas
- "Create a resourcequota?" -> POST /api/v1/namespaces/{namespace}/resourcequotas
- "Delete a resourcequota?" -> DELETE /api/v1/namespaces/{namespace}/resourcequotas/{name}
- "Get resourcequota details?" -> GET /api/v1/namespaces/{namespace}/resourcequotas/{name}
- "Partially update a resourcequota?" -> PATCH /api/v1/namespaces/{namespace}/resourcequotas/{name}
- "Update a resourcequota?" -> PUT /api/v1/namespaces/{namespace}/resourcequotas/{name}
- "List all status?" -> GET /api/v1/namespaces/{namespace}/resourcequotas/{name}/status
- "List all secrets?" -> GET /api/v1/namespaces/{namespace}/secrets
- "Create a secret?" -> POST /api/v1/namespaces/{namespace}/secrets
- "Delete a secret?" -> DELETE /api/v1/namespaces/{namespace}/secrets/{name}
- "Get secret details?" -> GET /api/v1/namespaces/{namespace}/secrets/{name}
- "Partially update a secret?" -> PATCH /api/v1/namespaces/{namespace}/secrets/{name}
- "Update a secret?" -> PUT /api/v1/namespaces/{namespace}/secrets/{name}
- "List all serviceaccounts?" -> GET /api/v1/namespaces/{namespace}/serviceaccounts
- "Create a serviceaccount?" -> POST /api/v1/namespaces/{namespace}/serviceaccounts
- "Delete a serviceaccount?" -> DELETE /api/v1/namespaces/{namespace}/serviceaccounts/{name}
- "Get serviceaccount details?" -> GET /api/v1/namespaces/{namespace}/serviceaccounts/{name}
- "Partially update a serviceaccount?" -> PATCH /api/v1/namespaces/{namespace}/serviceaccounts/{name}
- "Update a serviceaccount?" -> PUT /api/v1/namespaces/{namespace}/serviceaccounts/{name}
- "Create a token?" -> POST /api/v1/namespaces/{namespace}/serviceaccounts/{name}/token
- "List all services?" -> GET /api/v1/namespaces/{namespace}/services
- "Create a service?" -> POST /api/v1/namespaces/{namespace}/services
- "Delete a service?" -> DELETE /api/v1/namespaces/{namespace}/services/{name}
- "Get service details?" -> GET /api/v1/namespaces/{namespace}/services/{name}
- "Partially update a service?" -> PATCH /api/v1/namespaces/{namespace}/services/{name}
- "Update a service?" -> PUT /api/v1/namespaces/{namespace}/services/{name}
- "List all proxy?" -> GET /api/v1/namespaces/{namespace}/services/{name}/proxy
- "Create a proxy?" -> POST /api/v1/namespaces/{namespace}/services/{name}/proxy
- "Delete a proxy?" -> DELETE /api/v1/namespaces/{namespace}/services/{name}/proxy/{path}
- "Get proxy details?" -> GET /api/v1/namespaces/{namespace}/services/{name}/proxy/{path}
- "Partially update a proxy?" -> PATCH /api/v1/namespaces/{namespace}/services/{name}/proxy/{path}
- "Update a proxy?" -> PUT /api/v1/namespaces/{namespace}/services/{name}/proxy/{path}
- "List all status?" -> GET /api/v1/namespaces/{namespace}/services/{name}/status
- "Delete a namespace?" -> DELETE /api/v1/namespaces/{name}
- "Get namespace details?" -> GET /api/v1/namespaces/{name}
- "Partially update a namespace?" -> PATCH /api/v1/namespaces/{name}
- "Update a namespace?" -> PUT /api/v1/namespaces/{name}
- "List all status?" -> GET /api/v1/namespaces/{name}/status
- "List all nodes?" -> GET /api/v1/nodes
- "Create a node?" -> POST /api/v1/nodes
- "Delete a node?" -> DELETE /api/v1/nodes/{name}
- "Get node details?" -> GET /api/v1/nodes/{name}
- "Partially update a node?" -> PATCH /api/v1/nodes/{name}
- "Update a node?" -> PUT /api/v1/nodes/{name}
- "List all proxy?" -> GET /api/v1/nodes/{name}/proxy
- "Create a proxy?" -> POST /api/v1/nodes/{name}/proxy
- "Delete a proxy?" -> DELETE /api/v1/nodes/{name}/proxy/{path}
- "Get proxy details?" -> GET /api/v1/nodes/{name}/proxy/{path}
- "Partially update a proxy?" -> PATCH /api/v1/nodes/{name}/proxy/{path}
- "Update a proxy?" -> PUT /api/v1/nodes/{name}/proxy/{path}
- "List all status?" -> GET /api/v1/nodes/{name}/status
- "List all persistentvolumeclaims?" -> GET /api/v1/persistentvolumeclaims
- "List all persistentvolumes?" -> GET /api/v1/persistentvolumes
- "Create a persistentvolume?" -> POST /api/v1/persistentvolumes
- "Delete a persistentvolume?" -> DELETE /api/v1/persistentvolumes/{name}
- "Get persistentvolume details?" -> GET /api/v1/persistentvolumes/{name}
- "Partially update a persistentvolume?" -> PATCH /api/v1/persistentvolumes/{name}
- "Update a persistentvolume?" -> PUT /api/v1/persistentvolumes/{name}
- "List all status?" -> GET /api/v1/persistentvolumes/{name}/status
- "List all pods?" -> GET /api/v1/pods
- "List all podtemplates?" -> GET /api/v1/podtemplates
- "List all replicationcontrollers?" -> GET /api/v1/replicationcontrollers
- "List all resourcequotas?" -> GET /api/v1/resourcequotas
- "List all secrets?" -> GET /api/v1/secrets
- "List all serviceaccounts?" -> GET /api/v1/serviceaccounts
- "List all services?" -> GET /api/v1/services
- "List all configmaps?" -> GET /api/v1/watch/configmaps
- "List all endpoints?" -> GET /api/v1/watch/endpoints
- "List all events?" -> GET /api/v1/watch/events
- "List all limitranges?" -> GET /api/v1/watch/limitranges
- "List all namespaces?" -> GET /api/v1/watch/namespaces
- "List all configmaps?" -> GET /api/v1/watch/namespaces/{namespace}/configmaps
- "Get configmap details?" -> GET /api/v1/watch/namespaces/{namespace}/configmaps/{name}
- "List all endpoints?" -> GET /api/v1/watch/namespaces/{namespace}/endpoints
- "Get endpoint details?" -> GET /api/v1/watch/namespaces/{namespace}/endpoints/{name}
- "List all events?" -> GET /api/v1/watch/namespaces/{namespace}/events
- "Get event details?" -> GET /api/v1/watch/namespaces/{namespace}/events/{name}
- "List all limitranges?" -> GET /api/v1/watch/namespaces/{namespace}/limitranges
- "Get limitrange details?" -> GET /api/v1/watch/namespaces/{namespace}/limitranges/{name}
- "List all persistentvolumeclaims?" -> GET /api/v1/watch/namespaces/{namespace}/persistentvolumeclaims
- "Get persistentvolumeclaim details?" -> GET /api/v1/watch/namespaces/{namespace}/persistentvolumeclaims/{name}
- "List all pods?" -> GET /api/v1/watch/namespaces/{namespace}/pods
- "Get pod details?" -> GET /api/v1/watch/namespaces/{namespace}/pods/{name}
- "List all podtemplates?" -> GET /api/v1/watch/namespaces/{namespace}/podtemplates
- "Get podtemplate details?" -> GET /api/v1/watch/namespaces/{namespace}/podtemplates/{name}
- "List all replicationcontrollers?" -> GET /api/v1/watch/namespaces/{namespace}/replicationcontrollers
- "Get replicationcontroller details?" -> GET /api/v1/watch/namespaces/{namespace}/replicationcontrollers/{name}
- "List all resourcequotas?" -> GET /api/v1/watch/namespaces/{namespace}/resourcequotas
- "Get resourcequota details?" -> GET /api/v1/watch/namespaces/{namespace}/resourcequotas/{name}
- "List all secrets?" -> GET /api/v1/watch/namespaces/{namespace}/secrets
- "Get secret details?" -> GET /api/v1/watch/namespaces/{namespace}/secrets/{name}
- "List all serviceaccounts?" -> GET /api/v1/watch/namespaces/{namespace}/serviceaccounts
- "Get serviceaccount details?" -> GET /api/v1/watch/namespaces/{namespace}/serviceaccounts/{name}
- "List all services?" -> GET /api/v1/watch/namespaces/{namespace}/services
- "Get service details?" -> GET /api/v1/watch/namespaces/{namespace}/services/{name}
- "Get namespace details?" -> GET /api/v1/watch/namespaces/{name}
- "List all nodes?" -> GET /api/v1/watch/nodes
- "Get node details?" -> GET /api/v1/watch/nodes/{name}
- "List all persistentvolumeclaims?" -> GET /api/v1/watch/persistentvolumeclaims
- "List all persistentvolumes?" -> GET /api/v1/watch/persistentvolumes
- "Get persistentvolume details?" -> GET /api/v1/watch/persistentvolumes/{name}
- "List all pods?" -> GET /api/v1/watch/pods
- "List all podtemplates?" -> GET /api/v1/watch/podtemplates
- "List all replicationcontrollers?" -> GET /api/v1/watch/replicationcontrollers
- "List all resourcequotas?" -> GET /api/v1/watch/resourcequotas
- "List all secrets?" -> GET /api/v1/watch/secrets
- "List all serviceaccounts?" -> GET /api/v1/watch/serviceaccounts
- "List all services?" -> GET /api/v1/watch/services
- "List all apis?" -> GET /apis/
- "List all admissionregistration.k8s.io?" -> GET /apis/admissionregistration.k8s.io/
- "List all admissionregistration.k8s.io?" -> GET /apis/admissionregistration.k8s.io/v1/
- "List all mutatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies
- "Create a mutatingadmissionpolicy?" -> POST /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies
- "Delete a mutatingadmissionpolicy?" -> DELETE /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name}
- "Get mutatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name}
- "Partially update a mutatingadmissionpolicy?" -> PATCH /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name}
- "Update a mutatingadmissionpolicy?" -> PUT /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicies/{name}
- "List all mutatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings
- "Create a mutatingadmissionpolicybinding?" -> POST /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings
- "Delete a mutatingadmissionpolicybinding?" -> DELETE /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name}
- "Get mutatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name}
- "Partially update a mutatingadmissionpolicybinding?" -> PATCH /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name}
- "Update a mutatingadmissionpolicybinding?" -> PUT /apis/admissionregistration.k8s.io/v1/mutatingadmissionpolicybindings/{name}
- "List all mutatingwebhookconfigurations?" -> GET /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations
- "Create a mutatingwebhookconfiguration?" -> POST /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations
- "Delete a mutatingwebhookconfiguration?" -> DELETE /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name}
- "Get mutatingwebhookconfiguration details?" -> GET /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name}
- "Partially update a mutatingwebhookconfiguration?" -> PATCH /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name}
- "Update a mutatingwebhookconfiguration?" -> PUT /apis/admissionregistration.k8s.io/v1/mutatingwebhookconfigurations/{name}
- "List all validatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies
- "Create a validatingadmissionpolicy?" -> POST /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies
- "Delete a validatingadmissionpolicy?" -> DELETE /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}
- "Get validatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}
- "Partially update a validatingadmissionpolicy?" -> PATCH /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}
- "Update a validatingadmissionpolicy?" -> PUT /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}
- "List all status?" -> GET /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicies/{name}/status
- "List all validatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings
- "Create a validatingadmissionpolicybinding?" -> POST /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings
- "Delete a validatingadmissionpolicybinding?" -> DELETE /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name}
- "Get validatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name}
- "Partially update a validatingadmissionpolicybinding?" -> PATCH /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name}
- "Update a validatingadmissionpolicybinding?" -> PUT /apis/admissionregistration.k8s.io/v1/validatingadmissionpolicybindings/{name}
- "List all validatingwebhookconfigurations?" -> GET /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations
- "Create a validatingwebhookconfiguration?" -> POST /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations
- "Delete a validatingwebhookconfiguration?" -> DELETE /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name}
- "Get validatingwebhookconfiguration details?" -> GET /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name}
- "Partially update a validatingwebhookconfiguration?" -> PATCH /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name}
- "Update a validatingwebhookconfiguration?" -> PUT /apis/admissionregistration.k8s.io/v1/validatingwebhookconfigurations/{name}
- "List all mutatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicies
- "Get mutatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicies/{name}
- "List all mutatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicybindings
- "Get mutatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1/watch/mutatingadmissionpolicybindings/{name}
- "List all mutatingwebhookconfigurations?" -> GET /apis/admissionregistration.k8s.io/v1/watch/mutatingwebhookconfigurations
- "Get mutatingwebhookconfiguration details?" -> GET /apis/admissionregistration.k8s.io/v1/watch/mutatingwebhookconfigurations/{name}
- "List all validatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicies
- "Get validatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicies/{name}
- "List all validatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicybindings
- "Get validatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1/watch/validatingadmissionpolicybindings/{name}
- "List all validatingwebhookconfigurations?" -> GET /apis/admissionregistration.k8s.io/v1/watch/validatingwebhookconfigurations
- "Get validatingwebhookconfiguration details?" -> GET /apis/admissionregistration.k8s.io/v1/watch/validatingwebhookconfigurations/{name}
- "List all v1alpha1?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/
- "List all mutatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies
- "Create a mutatingadmissionpolicy?" -> POST /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies
- "Delete a mutatingadmissionpolicy?" -> DELETE /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name}
- "Get mutatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name}
- "Partially update a mutatingadmissionpolicy?" -> PATCH /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name}
- "Update a mutatingadmissionpolicy?" -> PUT /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicies/{name}
- "List all mutatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings
- "Create a mutatingadmissionpolicybinding?" -> POST /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings
- "Delete a mutatingadmissionpolicybinding?" -> DELETE /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name}
- "Get mutatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name}
- "Partially update a mutatingadmissionpolicybinding?" -> PATCH /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name}
- "Update a mutatingadmissionpolicybinding?" -> PUT /apis/admissionregistration.k8s.io/v1alpha1/mutatingadmissionpolicybindings/{name}
- "List all mutatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicies
- "Get mutatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicies/{name}
- "List all mutatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicybindings
- "Get mutatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1alpha1/watch/mutatingadmissionpolicybindings/{name}
- "List all v1beta1?" -> GET /apis/admissionregistration.k8s.io/v1beta1/
- "List all mutatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies
- "Create a mutatingadmissionpolicy?" -> POST /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies
- "Delete a mutatingadmissionpolicy?" -> DELETE /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name}
- "Get mutatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name}
- "Partially update a mutatingadmissionpolicy?" -> PATCH /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name}
- "Update a mutatingadmissionpolicy?" -> PUT /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicies/{name}
- "List all mutatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings
- "Create a mutatingadmissionpolicybinding?" -> POST /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings
- "Delete a mutatingadmissionpolicybinding?" -> DELETE /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name}
- "Get mutatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name}
- "Partially update a mutatingadmissionpolicybinding?" -> PATCH /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name}
- "Update a mutatingadmissionpolicybinding?" -> PUT /apis/admissionregistration.k8s.io/v1beta1/mutatingadmissionpolicybindings/{name}
- "List all mutatingadmissionpolicies?" -> GET /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicies
- "Get mutatingadmissionpolicy details?" -> GET /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicies/{name}
- "List all mutatingadmissionpolicybindings?" -> GET /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicybindings
- "Get mutatingadmissionpolicybinding details?" -> GET /apis/admissionregistration.k8s.io/v1beta1/watch/mutatingadmissionpolicybindings/{name}
- "List all apiextensions.k8s.io?" -> GET /apis/apiextensions.k8s.io/
- "List all apiextensions.k8s.io?" -> GET /apis/apiextensions.k8s.io/v1/
- "List all customresourcedefinitions?" -> GET /apis/apiextensions.k8s.io/v1/customresourcedefinitions
- "Create a customresourcedefinition?" -> POST /apis/apiextensions.k8s.io/v1/customresourcedefinitions
- "Delete a customresourcedefinition?" -> DELETE /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}
- "Get customresourcedefinition details?" -> GET /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}
- "Partially update a customresourcedefinition?" -> PATCH /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}
- "Update a customresourcedefinition?" -> PUT /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}
- "List all status?" -> GET /apis/apiextensions.k8s.io/v1/customresourcedefinitions/{name}/status
- "List all customresourcedefinitions?" -> GET /apis/apiextensions.k8s.io/v1/watch/customresourcedefinitions
- "Get customresourcedefinition details?" -> GET /apis/apiextensions.k8s.io/v1/watch/customresourcedefinitions/{name}
- "List all apiregistration.k8s.io?" -> GET /apis/apiregistration.k8s.io/
- "List all apiregistration.k8s.io?" -> GET /apis/apiregistration.k8s.io/v1/
- "List all apiservices?" -> GET /apis/apiregistration.k8s.io/v1/apiservices
- "Create a apiservice?" -> POST /apis/apiregistration.k8s.io/v1/apiservices
- "Delete a apiservice?" -> DELETE /apis/apiregistration.k8s.io/v1/apiservices/{name}
- "Get apiservice details?" -> GET /apis/apiregistration.k8s.io/v1/apiservices/{name}
- "Partially update a apiservice?" -> PATCH /apis/apiregistration.k8s.io/v1/apiservices/{name}
- "Update a apiservice?" -> PUT /apis/apiregistration.k8s.io/v1/apiservices/{name}
- "List all status?" -> GET /apis/apiregistration.k8s.io/v1/apiservices/{name}/status
- "List all apiservices?" -> GET /apis/apiregistration.k8s.io/v1/watch/apiservices
- "Get apiservice details?" -> GET /apis/apiregistration.k8s.io/v1/watch/apiservices/{name}
- "List all apps?" -> GET /apis/apps/
- "List all apps?" -> GET /apis/apps/v1/
- "List all controllerrevisions?" -> GET /apis/apps/v1/controllerrevisions
- "List all daemonsets?" -> GET /apis/apps/v1/daemonsets
- "List all deployments?" -> GET /apis/apps/v1/deployments
- "List all controllerrevisions?" -> GET /apis/apps/v1/namespaces/{namespace}/controllerrevisions
- "Create a controllerrevision?" -> POST /apis/apps/v1/namespaces/{namespace}/controllerrevisions
- "Delete a controllerrevision?" -> DELETE /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name}
- "Get controllerrevision details?" -> GET /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name}
- "Partially update a controllerrevision?" -> PATCH /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name}
- "Update a controllerrevision?" -> PUT /apis/apps/v1/namespaces/{namespace}/controllerrevisions/{name}
- "List all daemonsets?" -> GET /apis/apps/v1/namespaces/{namespace}/daemonsets
- "Create a daemonset?" -> POST /apis/apps/v1/namespaces/{namespace}/daemonsets
- "Delete a daemonset?" -> DELETE /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}
- "Get daemonset details?" -> GET /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}
- "Partially update a daemonset?" -> PATCH /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}
- "Update a daemonset?" -> PUT /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}
- "List all status?" -> GET /apis/apps/v1/namespaces/{namespace}/daemonsets/{name}/status
- "List all deployments?" -> GET /apis/apps/v1/namespaces/{namespace}/deployments
- "Create a deployment?" -> POST /apis/apps/v1/namespaces/{namespace}/deployments
- "Delete a deployment?" -> DELETE /apis/apps/v1/namespaces/{namespace}/deployments/{name}
- "Get deployment details?" -> GET /apis/apps/v1/namespaces/{namespace}/deployments/{name}
- "Partially update a deployment?" -> PATCH /apis/apps/v1/namespaces/{namespace}/deployments/{name}
- "Update a deployment?" -> PUT /apis/apps/v1/namespaces/{namespace}/deployments/{name}
- "List all scale?" -> GET /apis/apps/v1/namespaces/{namespace}/deployments/{name}/scale
- "List all status?" -> GET /apis/apps/v1/namespaces/{namespace}/deployments/{name}/status
- "List all replicasets?" -> GET /apis/apps/v1/namespaces/{namespace}/replicasets
- "Create a replicaset?" -> POST /apis/apps/v1/namespaces/{namespace}/replicasets
- "Delete a replicaset?" -> DELETE /apis/apps/v1/namespaces/{namespace}/replicasets/{name}
- "Get replicaset details?" -> GET /apis/apps/v1/namespaces/{namespace}/replicasets/{name}
- "Partially update a replicaset?" -> PATCH /apis/apps/v1/namespaces/{namespace}/replicasets/{name}
- "Update a replicaset?" -> PUT /apis/apps/v1/namespaces/{namespace}/replicasets/{name}
- "List all scale?" -> GET /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/scale
- "List all status?" -> GET /apis/apps/v1/namespaces/{namespace}/replicasets/{name}/status
- "List all statefulsets?" -> GET /apis/apps/v1/namespaces/{namespace}/statefulsets
- "Create a statefulset?" -> POST /apis/apps/v1/namespaces/{namespace}/statefulsets
- "Delete a statefulset?" -> DELETE /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}
- "Get statefulset details?" -> GET /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}
- "Partially update a statefulset?" -> PATCH /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}
- "Update a statefulset?" -> PUT /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}
- "List all scale?" -> GET /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/scale
- "List all status?" -> GET /apis/apps/v1/namespaces/{namespace}/statefulsets/{name}/status
- "List all replicasets?" -> GET /apis/apps/v1/replicasets
- "List all statefulsets?" -> GET /apis/apps/v1/statefulsets
- "List all controllerrevisions?" -> GET /apis/apps/v1/watch/controllerrevisions
- "List all daemonsets?" -> GET /apis/apps/v1/watch/daemonsets
- "List all deployments?" -> GET /apis/apps/v1/watch/deployments
- "List all controllerrevisions?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/controllerrevisions
- "Get controllerrevision details?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/controllerrevisions/{name}
- "List all daemonsets?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/daemonsets
- "Get daemonset details?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/daemonsets/{name}
- "List all deployments?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/deployments
- "Get deployment details?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/deployments/{name}
- "List all replicasets?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/replicasets
- "Get replicaset details?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/replicasets/{name}
- "List all statefulsets?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/statefulsets
- "Get statefulset details?" -> GET /apis/apps/v1/watch/namespaces/{namespace}/statefulsets/{name}
- "List all replicasets?" -> GET /apis/apps/v1/watch/replicasets
- "List all statefulsets?" -> GET /apis/apps/v1/watch/statefulsets
- "List all authentication.k8s.io?" -> GET /apis/authentication.k8s.io/
- "List all authentication.k8s.io?" -> GET /apis/authentication.k8s.io/v1/
- "Create a selfsubjectreview?" -> POST /apis/authentication.k8s.io/v1/selfsubjectreviews
- "Create a tokenreview?" -> POST /apis/authentication.k8s.io/v1/tokenreviews
- "List all authorization.k8s.io?" -> GET /apis/authorization.k8s.io/
- "List all authorization.k8s.io?" -> GET /apis/authorization.k8s.io/v1/
- "Create a localsubjectaccessreview?" -> POST /apis/authorization.k8s.io/v1/namespaces/{namespace}/localsubjectaccessreviews
- "Create a selfsubjectaccessreview?" -> POST /apis/authorization.k8s.io/v1/selfsubjectaccessreviews
- "Create a selfsubjectrulesreview?" -> POST /apis/authorization.k8s.io/v1/selfsubjectrulesreviews
- "Create a subjectaccessreview?" -> POST /apis/authorization.k8s.io/v1/subjectaccessreviews
- "List all autoscaling?" -> GET /apis/autoscaling/
- "List all autoscaling?" -> GET /apis/autoscaling/v1/
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v1/horizontalpodautoscalers
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers
- "Create a horizontalpodautoscaler?" -> POST /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers
- "Delete a horizontalpodautoscaler?" -> DELETE /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "Get horizontalpodautoscaler details?" -> GET /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "Partially update a horizontalpodautoscaler?" -> PATCH /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "Update a horizontalpodautoscaler?" -> PUT /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "List all status?" -> GET /apis/autoscaling/v1/namespaces/{namespace}/horizontalpodautoscalers/{name}/status
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v1/watch/horizontalpodautoscalers
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v1/watch/namespaces/{namespace}/horizontalpodautoscalers
- "Get horizontalpodautoscaler details?" -> GET /apis/autoscaling/v1/watch/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "List all autoscaling?" -> GET /apis/autoscaling/v2/
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v2/horizontalpodautoscalers
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers
- "Create a horizontalpodautoscaler?" -> POST /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers
- "Delete a horizontalpodautoscaler?" -> DELETE /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "Get horizontalpodautoscaler details?" -> GET /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "Partially update a horizontalpodautoscaler?" -> PATCH /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "Update a horizontalpodautoscaler?" -> PUT /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "List all status?" -> GET /apis/autoscaling/v2/namespaces/{namespace}/horizontalpodautoscalers/{name}/status
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v2/watch/horizontalpodautoscalers
- "List all horizontalpodautoscalers?" -> GET /apis/autoscaling/v2/watch/namespaces/{namespace}/horizontalpodautoscalers
- "Get horizontalpodautoscaler details?" -> GET /apis/autoscaling/v2/watch/namespaces/{namespace}/horizontalpodautoscalers/{name}
- "List all batch?" -> GET /apis/batch/
- "List all batch?" -> GET /apis/batch/v1/
- "List all cronjobs?" -> GET /apis/batch/v1/cronjobs
- "List all jobs?" -> GET /apis/batch/v1/jobs
- "List all cronjobs?" -> GET /apis/batch/v1/namespaces/{namespace}/cronjobs
- "Create a cronjob?" -> POST /apis/batch/v1/namespaces/{namespace}/cronjobs
- "Delete a cronjob?" -> DELETE /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}
- "Get cronjob details?" -> GET /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}
- "Partially update a cronjob?" -> PATCH /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}
- "Update a cronjob?" -> PUT /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}
- "List all status?" -> GET /apis/batch/v1/namespaces/{namespace}/cronjobs/{name}/status
- "List all jobs?" -> GET /apis/batch/v1/namespaces/{namespace}/jobs
- "Create a job?" -> POST /apis/batch/v1/namespaces/{namespace}/jobs
- "Delete a job?" -> DELETE /apis/batch/v1/namespaces/{namespace}/jobs/{name}
- "Get job details?" -> GET /apis/batch/v1/namespaces/{namespace}/jobs/{name}
- "Partially update a job?" -> PATCH /apis/batch/v1/namespaces/{namespace}/jobs/{name}
- "Update a job?" -> PUT /apis/batch/v1/namespaces/{namespace}/jobs/{name}
- "List all status?" -> GET /apis/batch/v1/namespaces/{namespace}/jobs/{name}/status
- "List all cronjobs?" -> GET /apis/batch/v1/watch/cronjobs
- "List all jobs?" -> GET /apis/batch/v1/watch/jobs
- "List all cronjobs?" -> GET /apis/batch/v1/watch/namespaces/{namespace}/cronjobs
- "Get cronjob details?" -> GET /apis/batch/v1/watch/namespaces/{namespace}/cronjobs/{name}
- "List all jobs?" -> GET /apis/batch/v1/watch/namespaces/{namespace}/jobs
- "Get job details?" -> GET /apis/batch/v1/watch/namespaces/{namespace}/jobs/{name}
- "List all certificates.k8s.io?" -> GET /apis/certificates.k8s.io/
- "List all certificates.k8s.io?" -> GET /apis/certificates.k8s.io/v1/
- "List all certificatesigningrequests?" -> GET /apis/certificates.k8s.io/v1/certificatesigningrequests
- "Create a certificatesigningrequest?" -> POST /apis/certificates.k8s.io/v1/certificatesigningrequests
- "Delete a certificatesigningrequest?" -> DELETE /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}
- "Get certificatesigningrequest details?" -> GET /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}
- "Partially update a certificatesigningrequest?" -> PATCH /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}
- "Update a certificatesigningrequest?" -> PUT /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}
- "List all approval?" -> GET /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/approval
- "List all status?" -> GET /apis/certificates.k8s.io/v1/certificatesigningrequests/{name}/status
- "List all certificatesigningrequests?" -> GET /apis/certificates.k8s.io/v1/watch/certificatesigningrequests
- "Get certificatesigningrequest details?" -> GET /apis/certificates.k8s.io/v1/watch/certificatesigningrequests/{name}
- "List all v1alpha1?" -> GET /apis/certificates.k8s.io/v1alpha1/
- "List all clustertrustbundles?" -> GET /apis/certificates.k8s.io/v1alpha1/clustertrustbundles
- "Create a clustertrustbundle?" -> POST /apis/certificates.k8s.io/v1alpha1/clustertrustbundles
- "Delete a clustertrustbundle?" -> DELETE /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name}
- "Get clustertrustbundle details?" -> GET /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name}
- "Partially update a clustertrustbundle?" -> PATCH /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name}
- "Update a clustertrustbundle?" -> PUT /apis/certificates.k8s.io/v1alpha1/clustertrustbundles/{name}
- "List all clustertrustbundles?" -> GET /apis/certificates.k8s.io/v1alpha1/watch/clustertrustbundles
- "Get clustertrustbundle details?" -> GET /apis/certificates.k8s.io/v1alpha1/watch/clustertrustbundles/{name}
- "List all v1beta1?" -> GET /apis/certificates.k8s.io/v1beta1/
- "List all clustertrustbundles?" -> GET /apis/certificates.k8s.io/v1beta1/clustertrustbundles
- "Create a clustertrustbundle?" -> POST /apis/certificates.k8s.io/v1beta1/clustertrustbundles
- "Delete a clustertrustbundle?" -> DELETE /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name}
- "Get clustertrustbundle details?" -> GET /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name}
- "Partially update a clustertrustbundle?" -> PATCH /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name}
- "Update a clustertrustbundle?" -> PUT /apis/certificates.k8s.io/v1beta1/clustertrustbundles/{name}
- "List all podcertificaterequests?" -> GET /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests
- "Create a podcertificaterequest?" -> POST /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests
- "Delete a podcertificaterequest?" -> DELETE /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}
- "Get podcertificaterequest details?" -> GET /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}
- "Partially update a podcertificaterequest?" -> PATCH /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}
- "Update a podcertificaterequest?" -> PUT /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}
- "List all status?" -> GET /apis/certificates.k8s.io/v1beta1/namespaces/{namespace}/podcertificaterequests/{name}/status
- "List all podcertificaterequests?" -> GET /apis/certificates.k8s.io/v1beta1/podcertificaterequests
- "List all clustertrustbundles?" -> GET /apis/certificates.k8s.io/v1beta1/watch/clustertrustbundles
- "Get clustertrustbundle details?" -> GET /apis/certificates.k8s.io/v1beta1/watch/clustertrustbundles/{name}
- "List all podcertificaterequests?" -> GET /apis/certificates.k8s.io/v1beta1/watch/namespaces/{namespace}/podcertificaterequests
- "Get podcertificaterequest details?" -> GET /apis/certificates.k8s.io/v1beta1/watch/namespaces/{namespace}/podcertificaterequests/{name}
- "List all podcertificaterequests?" -> GET /apis/certificates.k8s.io/v1beta1/watch/podcertificaterequests
- "List all coordination.k8s.io?" -> GET /apis/coordination.k8s.io/
- "List all coordination.k8s.io?" -> GET /apis/coordination.k8s.io/v1/
- "List all leases?" -> GET /apis/coordination.k8s.io/v1/leases
- "List all leases?" -> GET /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases
- "Create a lease?" -> POST /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases
- "Delete a lease?" -> DELETE /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}
- "Get lease details?" -> GET /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}
- "Partially update a lease?" -> PATCH /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}
- "Update a lease?" -> PUT /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}
- "List all leases?" -> GET /apis/coordination.k8s.io/v1/watch/leases
- "List all leases?" -> GET /apis/coordination.k8s.io/v1/watch/namespaces/{namespace}/leases
- "Get lease details?" -> GET /apis/coordination.k8s.io/v1/watch/namespaces/{namespace}/leases/{name}
- "List all v1alpha2?" -> GET /apis/coordination.k8s.io/v1alpha2/
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1alpha2/leasecandidates
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates
- "Create a leasecandidate?" -> POST /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates
- "Delete a leasecandidate?" -> DELETE /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name}
- "Get leasecandidate details?" -> GET /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name}
- "Partially update a leasecandidate?" -> PATCH /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name}
- "Update a leasecandidate?" -> PUT /apis/coordination.k8s.io/v1alpha2/namespaces/{namespace}/leasecandidates/{name}
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1alpha2/watch/leasecandidates
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1alpha2/watch/namespaces/{namespace}/leasecandidates
- "Get leasecandidate details?" -> GET /apis/coordination.k8s.io/v1alpha2/watch/namespaces/{namespace}/leasecandidates/{name}
- "List all v1beta1?" -> GET /apis/coordination.k8s.io/v1beta1/
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1beta1/leasecandidates
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates
- "Create a leasecandidate?" -> POST /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates
- "Delete a leasecandidate?" -> DELETE /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name}
- "Get leasecandidate details?" -> GET /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name}
- "Partially update a leasecandidate?" -> PATCH /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name}
- "Update a leasecandidate?" -> PUT /apis/coordination.k8s.io/v1beta1/namespaces/{namespace}/leasecandidates/{name}
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1beta1/watch/leasecandidates
- "List all leasecandidates?" -> GET /apis/coordination.k8s.io/v1beta1/watch/namespaces/{namespace}/leasecandidates
- "Get leasecandidate details?" -> GET /apis/coordination.k8s.io/v1beta1/watch/namespaces/{namespace}/leasecandidates/{name}
- "List all discovery.k8s.io?" -> GET /apis/discovery.k8s.io/
- "List all discovery.k8s.io?" -> GET /apis/discovery.k8s.io/v1/
- "List all endpointslices?" -> GET /apis/discovery.k8s.io/v1/endpointslices
- "List all endpointslices?" -> GET /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices
- "Create a endpointslice?" -> POST /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices
- "Delete a endpointslice?" -> DELETE /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name}
- "Get endpointslice details?" -> GET /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name}
- "Partially update a endpointslice?" -> PATCH /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name}
- "Update a endpointslice?" -> PUT /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices/{name}
- "List all endpointslices?" -> GET /apis/discovery.k8s.io/v1/watch/endpointslices
- "List all endpointslices?" -> GET /apis/discovery.k8s.io/v1/watch/namespaces/{namespace}/endpointslices
- "Get endpointslice details?" -> GET /apis/discovery.k8s.io/v1/watch/namespaces/{namespace}/endpointslices/{name}
- "List all events.k8s.io?" -> GET /apis/events.k8s.io/
- "List all events.k8s.io?" -> GET /apis/events.k8s.io/v1/
- "List all events?" -> GET /apis/events.k8s.io/v1/events
- "List all events?" -> GET /apis/events.k8s.io/v1/namespaces/{namespace}/events
- "Create a event?" -> POST /apis/events.k8s.io/v1/namespaces/{namespace}/events
- "Delete a event?" -> DELETE /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name}
- "Get event details?" -> GET /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name}
- "Partially update a event?" -> PATCH /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name}
- "Update a event?" -> PUT /apis/events.k8s.io/v1/namespaces/{namespace}/events/{name}
- "List all events?" -> GET /apis/events.k8s.io/v1/watch/events
- "List all events?" -> GET /apis/events.k8s.io/v1/watch/namespaces/{namespace}/events
- "Get event details?" -> GET /apis/events.k8s.io/v1/watch/namespaces/{namespace}/events/{name}
- "List all flowcontrol.apiserver.k8s.io?" -> GET /apis/flowcontrol.apiserver.k8s.io/
- "List all flowcontrol.apiserver.k8s.io?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/
- "List all flowschemas?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas
- "Create a flowschema?" -> POST /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas
- "Delete a flowschema?" -> DELETE /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}
- "Get flowschema details?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}
- "Partially update a flowschema?" -> PATCH /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}
- "Update a flowschema?" -> PUT /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}
- "List all status?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/flowschemas/{name}/status
- "List all prioritylevelconfigurations?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations
- "Create a prioritylevelconfiguration?" -> POST /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations
- "Delete a prioritylevelconfiguration?" -> DELETE /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}
- "Get prioritylevelconfiguration details?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}
- "Partially update a prioritylevelconfiguration?" -> PATCH /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}
- "Update a prioritylevelconfiguration?" -> PUT /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}
- "List all status?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/prioritylevelconfigurations/{name}/status
- "List all flowschemas?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/watch/flowschemas
- "Get flowschema details?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/watch/flowschemas/{name}
- "List all prioritylevelconfigurations?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/watch/prioritylevelconfigurations
- "Get prioritylevelconfiguration details?" -> GET /apis/flowcontrol.apiserver.k8s.io/v1/watch/prioritylevelconfigurations/{name}
- "List all internal.apiserver.k8s.io?" -> GET /apis/internal.apiserver.k8s.io/
- "List all v1alpha1?" -> GET /apis/internal.apiserver.k8s.io/v1alpha1/
- "List all storageversions?" -> GET /apis/internal.apiserver.k8s.io/v1alpha1/storageversions
- "Create a storageversion?" -> POST /apis/internal.apiserver.k8s.io/v1alpha1/storageversions
- "Delete a storageversion?" -> DELETE /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}
- "Get storageversion details?" -> GET /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}
- "Partially update a storageversion?" -> PATCH /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}
- "Update a storageversion?" -> PUT /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}
- "List all status?" -> GET /apis/internal.apiserver.k8s.io/v1alpha1/storageversions/{name}/status
- "List all storageversions?" -> GET /apis/internal.apiserver.k8s.io/v1alpha1/watch/storageversions
- "Get storageversion details?" -> GET /apis/internal.apiserver.k8s.io/v1alpha1/watch/storageversions/{name}
- "List all networking.k8s.io?" -> GET /apis/networking.k8s.io/
- "List all networking.k8s.io?" -> GET /apis/networking.k8s.io/v1/
- "List all ingressclasses?" -> GET /apis/networking.k8s.io/v1/ingressclasses
- "Create a ingressclass?" -> POST /apis/networking.k8s.io/v1/ingressclasses
- "Delete a ingressclass?" -> DELETE /apis/networking.k8s.io/v1/ingressclasses/{name}
- "Get ingressclass details?" -> GET /apis/networking.k8s.io/v1/ingressclasses/{name}
- "Partially update a ingressclass?" -> PATCH /apis/networking.k8s.io/v1/ingressclasses/{name}
- "Update a ingressclass?" -> PUT /apis/networking.k8s.io/v1/ingressclasses/{name}
- "List all ingresses?" -> GET /apis/networking.k8s.io/v1/ingresses
- "List all ipaddresses?" -> GET /apis/networking.k8s.io/v1/ipaddresses
- "Create a ipaddress?" -> POST /apis/networking.k8s.io/v1/ipaddresses
- "Delete a ipaddress?" -> DELETE /apis/networking.k8s.io/v1/ipaddresses/{name}
- "Get ipaddress details?" -> GET /apis/networking.k8s.io/v1/ipaddresses/{name}
- "Partially update a ipaddress?" -> PATCH /apis/networking.k8s.io/v1/ipaddresses/{name}
- "Update a ipaddress?" -> PUT /apis/networking.k8s.io/v1/ipaddresses/{name}
- "List all ingresses?" -> GET /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses
- "Create a ingress?" -> POST /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses
- "Delete a ingress?" -> DELETE /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}
- "Get ingress details?" -> GET /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}
- "Partially update a ingress?" -> PATCH /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}
- "Update a ingress?" -> PUT /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}
- "List all status?" -> GET /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses/{name}/status
- "List all networkpolicies?" -> GET /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies
- "Create a networkpolicy?" -> POST /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies
- "Delete a networkpolicy?" -> DELETE /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name}
- "Get networkpolicy details?" -> GET /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name}
- "Partially update a networkpolicy?" -> PATCH /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name}
- "Update a networkpolicy?" -> PUT /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies/{name}
- "List all networkpolicies?" -> GET /apis/networking.k8s.io/v1/networkpolicies
- "List all servicecidrs?" -> GET /apis/networking.k8s.io/v1/servicecidrs
- "Create a servicecidr?" -> POST /apis/networking.k8s.io/v1/servicecidrs
- "Delete a servicecidr?" -> DELETE /apis/networking.k8s.io/v1/servicecidrs/{name}
- "Get servicecidr details?" -> GET /apis/networking.k8s.io/v1/servicecidrs/{name}
- "Partially update a servicecidr?" -> PATCH /apis/networking.k8s.io/v1/servicecidrs/{name}
- "Update a servicecidr?" -> PUT /apis/networking.k8s.io/v1/servicecidrs/{name}
- "List all status?" -> GET /apis/networking.k8s.io/v1/servicecidrs/{name}/status
- "List all ingressclasses?" -> GET /apis/networking.k8s.io/v1/watch/ingressclasses
- "Get ingressclass details?" -> GET /apis/networking.k8s.io/v1/watch/ingressclasses/{name}
- "List all ingresses?" -> GET /apis/networking.k8s.io/v1/watch/ingresses
- "List all ipaddresses?" -> GET /apis/networking.k8s.io/v1/watch/ipaddresses
- "Get ipaddress details?" -> GET /apis/networking.k8s.io/v1/watch/ipaddresses/{name}
- "List all ingresses?" -> GET /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/ingresses
- "Get ingress details?" -> GET /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/ingresses/{name}
- "List all networkpolicies?" -> GET /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/networkpolicies
- "Get networkpolicy details?" -> GET /apis/networking.k8s.io/v1/watch/namespaces/{namespace}/networkpolicies/{name}
- "List all networkpolicies?" -> GET /apis/networking.k8s.io/v1/watch/networkpolicies
- "List all servicecidrs?" -> GET /apis/networking.k8s.io/v1/watch/servicecidrs
- "Get servicecidr details?" -> GET /apis/networking.k8s.io/v1/watch/servicecidrs/{name}
- "List all v1beta1?" -> GET /apis/networking.k8s.io/v1beta1/
- "List all ipaddresses?" -> GET /apis/networking.k8s.io/v1beta1/ipaddresses
- "Create a ipaddress?" -> POST /apis/networking.k8s.io/v1beta1/ipaddresses
- "Delete a ipaddress?" -> DELETE /apis/networking.k8s.io/v1beta1/ipaddresses/{name}
- "Get ipaddress details?" -> GET /apis/networking.k8s.io/v1beta1/ipaddresses/{name}
- "Partially update a ipaddress?" -> PATCH /apis/networking.k8s.io/v1beta1/ipaddresses/{name}
- "Update a ipaddress?" -> PUT /apis/networking.k8s.io/v1beta1/ipaddresses/{name}
- "List all servicecidrs?" -> GET /apis/networking.k8s.io/v1beta1/servicecidrs
- "Create a servicecidr?" -> POST /apis/networking.k8s.io/v1beta1/servicecidrs
- "Delete a servicecidr?" -> DELETE /apis/networking.k8s.io/v1beta1/servicecidrs/{name}
- "Get servicecidr details?" -> GET /apis/networking.k8s.io/v1beta1/servicecidrs/{name}
- "Partially update a servicecidr?" -> PATCH /apis/networking.k8s.io/v1beta1/servicecidrs/{name}
- "Update a servicecidr?" -> PUT /apis/networking.k8s.io/v1beta1/servicecidrs/{name}
- "List all status?" -> GET /apis/networking.k8s.io/v1beta1/servicecidrs/{name}/status
- "List all ipaddresses?" -> GET /apis/networking.k8s.io/v1beta1/watch/ipaddresses
- "Get ipaddress details?" -> GET /apis/networking.k8s.io/v1beta1/watch/ipaddresses/{name}
- "List all servicecidrs?" -> GET /apis/networking.k8s.io/v1beta1/watch/servicecidrs
- "Get servicecidr details?" -> GET /apis/networking.k8s.io/v1beta1/watch/servicecidrs/{name}
- "List all node.k8s.io?" -> GET /apis/node.k8s.io/
- "List all node.k8s.io?" -> GET /apis/node.k8s.io/v1/
- "List all runtimeclasses?" -> GET /apis/node.k8s.io/v1/runtimeclasses
- "Create a runtimeclass?" -> POST /apis/node.k8s.io/v1/runtimeclasses
- "Delete a runtimeclass?" -> DELETE /apis/node.k8s.io/v1/runtimeclasses/{name}
- "Get runtimeclass details?" -> GET /apis/node.k8s.io/v1/runtimeclasses/{name}
- "Partially update a runtimeclass?" -> PATCH /apis/node.k8s.io/v1/runtimeclasses/{name}
- "Update a runtimeclass?" -> PUT /apis/node.k8s.io/v1/runtimeclasses/{name}
- "List all runtimeclasses?" -> GET /apis/node.k8s.io/v1/watch/runtimeclasses
- "Get runtimeclass details?" -> GET /apis/node.k8s.io/v1/watch/runtimeclasses/{name}
- "List all policy?" -> GET /apis/policy/
- "List all policy?" -> GET /apis/policy/v1/
- "List all poddisruptionbudgets?" -> GET /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets
- "Create a poddisruptionbudget?" -> POST /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets
- "Delete a poddisruptionbudget?" -> DELETE /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}
- "Get poddisruptionbudget details?" -> GET /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}
- "Partially update a poddisruptionbudget?" -> PATCH /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}
- "Update a poddisruptionbudget?" -> PUT /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}
- "List all status?" -> GET /apis/policy/v1/namespaces/{namespace}/poddisruptionbudgets/{name}/status
- "List all poddisruptionbudgets?" -> GET /apis/policy/v1/poddisruptionbudgets
- "List all poddisruptionbudgets?" -> GET /apis/policy/v1/watch/namespaces/{namespace}/poddisruptionbudgets
- "Get poddisruptionbudget details?" -> GET /apis/policy/v1/watch/namespaces/{namespace}/poddisruptionbudgets/{name}
- "List all poddisruptionbudgets?" -> GET /apis/policy/v1/watch/poddisruptionbudgets
- "List all rbac.authorization.k8s.io?" -> GET /apis/rbac.authorization.k8s.io/
- "List all rbac.authorization.k8s.io?" -> GET /apis/rbac.authorization.k8s.io/v1/
- "List all clusterrolebindings?" -> GET /apis/rbac.authorization.k8s.io/v1/clusterrolebindings
- "Create a clusterrolebinding?" -> POST /apis/rbac.authorization.k8s.io/v1/clusterrolebindings
- "Delete a clusterrolebinding?" -> DELETE /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}
- "Get clusterrolebinding details?" -> GET /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}
- "Partially update a clusterrolebinding?" -> PATCH /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}
- "Update a clusterrolebinding?" -> PUT /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}
- "List all clusterroles?" -> GET /apis/rbac.authorization.k8s.io/v1/clusterroles
- "Create a clusterrole?" -> POST /apis/rbac.authorization.k8s.io/v1/clusterroles
- "Delete a clusterrole?" -> DELETE /apis/rbac.authorization.k8s.io/v1/clusterroles/{name}
- "Get clusterrole details?" -> GET /apis/rbac.authorization.k8s.io/v1/clusterroles/{name}
- "Partially update a clusterrole?" -> PATCH /apis/rbac.authorization.k8s.io/v1/clusterroles/{name}
- "Update a clusterrole?" -> PUT /apis/rbac.authorization.k8s.io/v1/clusterroles/{name}
- "List all rolebindings?" -> GET /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings
- "Create a rolebinding?" -> POST /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings
- "Delete a rolebinding?" -> DELETE /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name}
- "Get rolebinding details?" -> GET /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name}
- "Partially update a rolebinding?" -> PATCH /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name}
- "Update a rolebinding?" -> PUT /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/rolebindings/{name}
- "List all roles?" -> GET /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles
- "Create a role?" -> POST /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles
- "Delete a role?" -> DELETE /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name}
- "Get role details?" -> GET /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name}
- "Partially update a role?" -> PATCH /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name}
- "Update a role?" -> PUT /apis/rbac.authorization.k8s.io/v1/namespaces/{namespace}/roles/{name}
- "List all rolebindings?" -> GET /apis/rbac.authorization.k8s.io/v1/rolebindings
- "List all roles?" -> GET /apis/rbac.authorization.k8s.io/v1/roles
- "List all clusterrolebindings?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/clusterrolebindings
- "Get clusterrolebinding details?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/clusterrolebindings/{name}
- "List all clusterroles?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/clusterroles
- "Get clusterrole details?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/clusterroles/{name}
- "List all rolebindings?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/rolebindings
- "Get rolebinding details?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/rolebindings/{name}
- "List all roles?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/roles
- "Get role details?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/namespaces/{namespace}/roles/{name}
- "List all rolebindings?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/rolebindings
- "List all roles?" -> GET /apis/rbac.authorization.k8s.io/v1/watch/roles
- "List all resource.k8s.io?" -> GET /apis/resource.k8s.io/
- "List all resource.k8s.io?" -> GET /apis/resource.k8s.io/v1/
- "List all deviceclasses?" -> GET /apis/resource.k8s.io/v1/deviceclasses
- "Create a deviceclass?" -> POST /apis/resource.k8s.io/v1/deviceclasses
- "Delete a deviceclass?" -> DELETE /apis/resource.k8s.io/v1/deviceclasses/{name}
- "Get deviceclass details?" -> GET /apis/resource.k8s.io/v1/deviceclasses/{name}
- "Partially update a deviceclass?" -> PATCH /apis/resource.k8s.io/v1/deviceclasses/{name}
- "Update a deviceclass?" -> PUT /apis/resource.k8s.io/v1/deviceclasses/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims
- "Create a resourceclaim?" -> POST /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims
- "Delete a resourceclaim?" -> DELETE /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}
- "Get resourceclaim details?" -> GET /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}
- "Partially update a resourceclaim?" -> PATCH /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}
- "Update a resourceclaim?" -> PUT /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}
- "List all status?" -> GET /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaims/{name}/status
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates
- "Create a resourceclaimtemplate?" -> POST /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates
- "Delete a resourceclaimtemplate?" -> DELETE /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Get resourceclaimtemplate details?" -> GET /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Partially update a resourceclaimtemplate?" -> PATCH /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Update a resourceclaimtemplate?" -> PUT /apis/resource.k8s.io/v1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1/resourceclaims
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1/resourceclaimtemplates
- "List all resourceslices?" -> GET /apis/resource.k8s.io/v1/resourceslices
- "Create a resourceslice?" -> POST /apis/resource.k8s.io/v1/resourceslices
- "Delete a resourceslice?" -> DELETE /apis/resource.k8s.io/v1/resourceslices/{name}
- "Get resourceslice details?" -> GET /apis/resource.k8s.io/v1/resourceslices/{name}
- "Partially update a resourceslice?" -> PATCH /apis/resource.k8s.io/v1/resourceslices/{name}
- "Update a resourceslice?" -> PUT /apis/resource.k8s.io/v1/resourceslices/{name}
- "List all deviceclasses?" -> GET /apis/resource.k8s.io/v1/watch/deviceclasses
- "Get deviceclass details?" -> GET /apis/resource.k8s.io/v1/watch/deviceclasses/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaims
- "Get resourceclaim details?" -> GET /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaims/{name}
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaimtemplates
- "Get resourceclaimtemplate details?" -> GET /apis/resource.k8s.io/v1/watch/namespaces/{namespace}/resourceclaimtemplates/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1/watch/resourceclaims
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1/watch/resourceclaimtemplates
- "List all resourceslices?" -> GET /apis/resource.k8s.io/v1/watch/resourceslices
- "Get resourceslice details?" -> GET /apis/resource.k8s.io/v1/watch/resourceslices/{name}
- "List all v1alpha3?" -> GET /apis/resource.k8s.io/v1alpha3/
- "List all devicetaintrules?" -> GET /apis/resource.k8s.io/v1alpha3/devicetaintrules
- "Create a devicetaintrule?" -> POST /apis/resource.k8s.io/v1alpha3/devicetaintrules
- "Delete a devicetaintrule?" -> DELETE /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}
- "Get devicetaintrule details?" -> GET /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}
- "Partially update a devicetaintrule?" -> PATCH /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}
- "Update a devicetaintrule?" -> PUT /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}
- "List all status?" -> GET /apis/resource.k8s.io/v1alpha3/devicetaintrules/{name}/status
- "List all devicetaintrules?" -> GET /apis/resource.k8s.io/v1alpha3/watch/devicetaintrules
- "Get devicetaintrule details?" -> GET /apis/resource.k8s.io/v1alpha3/watch/devicetaintrules/{name}
- "List all v1beta1?" -> GET /apis/resource.k8s.io/v1beta1/
- "List all deviceclasses?" -> GET /apis/resource.k8s.io/v1beta1/deviceclasses
- "Create a deviceclass?" -> POST /apis/resource.k8s.io/v1beta1/deviceclasses
- "Delete a deviceclass?" -> DELETE /apis/resource.k8s.io/v1beta1/deviceclasses/{name}
- "Get deviceclass details?" -> GET /apis/resource.k8s.io/v1beta1/deviceclasses/{name}
- "Partially update a deviceclass?" -> PATCH /apis/resource.k8s.io/v1beta1/deviceclasses/{name}
- "Update a deviceclass?" -> PUT /apis/resource.k8s.io/v1beta1/deviceclasses/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims
- "Create a resourceclaim?" -> POST /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims
- "Delete a resourceclaim?" -> DELETE /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}
- "Get resourceclaim details?" -> GET /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}
- "Partially update a resourceclaim?" -> PATCH /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}
- "Update a resourceclaim?" -> PUT /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}
- "List all status?" -> GET /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaims/{name}/status
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates
- "Create a resourceclaimtemplate?" -> POST /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates
- "Delete a resourceclaimtemplate?" -> DELETE /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Get resourceclaimtemplate details?" -> GET /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Partially update a resourceclaimtemplate?" -> PATCH /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Update a resourceclaimtemplate?" -> PUT /apis/resource.k8s.io/v1beta1/namespaces/{namespace}/resourceclaimtemplates/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta1/resourceclaims
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta1/resourceclaimtemplates
- "List all resourceslices?" -> GET /apis/resource.k8s.io/v1beta1/resourceslices
- "Create a resourceslice?" -> POST /apis/resource.k8s.io/v1beta1/resourceslices
- "Delete a resourceslice?" -> DELETE /apis/resource.k8s.io/v1beta1/resourceslices/{name}
- "Get resourceslice details?" -> GET /apis/resource.k8s.io/v1beta1/resourceslices/{name}
- "Partially update a resourceslice?" -> PATCH /apis/resource.k8s.io/v1beta1/resourceslices/{name}
- "Update a resourceslice?" -> PUT /apis/resource.k8s.io/v1beta1/resourceslices/{name}
- "List all deviceclasses?" -> GET /apis/resource.k8s.io/v1beta1/watch/deviceclasses
- "Get deviceclass details?" -> GET /apis/resource.k8s.io/v1beta1/watch/deviceclasses/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaims
- "Get resourceclaim details?" -> GET /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaims/{name}
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaimtemplates
- "Get resourceclaimtemplate details?" -> GET /apis/resource.k8s.io/v1beta1/watch/namespaces/{namespace}/resourceclaimtemplates/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta1/watch/resourceclaims
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta1/watch/resourceclaimtemplates
- "List all resourceslices?" -> GET /apis/resource.k8s.io/v1beta1/watch/resourceslices
- "Get resourceslice details?" -> GET /apis/resource.k8s.io/v1beta1/watch/resourceslices/{name}
- "List all v1beta2?" -> GET /apis/resource.k8s.io/v1beta2/
- "List all deviceclasses?" -> GET /apis/resource.k8s.io/v1beta2/deviceclasses
- "Create a deviceclass?" -> POST /apis/resource.k8s.io/v1beta2/deviceclasses
- "Delete a deviceclass?" -> DELETE /apis/resource.k8s.io/v1beta2/deviceclasses/{name}
- "Get deviceclass details?" -> GET /apis/resource.k8s.io/v1beta2/deviceclasses/{name}
- "Partially update a deviceclass?" -> PATCH /apis/resource.k8s.io/v1beta2/deviceclasses/{name}
- "Update a deviceclass?" -> PUT /apis/resource.k8s.io/v1beta2/deviceclasses/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims
- "Create a resourceclaim?" -> POST /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims
- "Delete a resourceclaim?" -> DELETE /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}
- "Get resourceclaim details?" -> GET /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}
- "Partially update a resourceclaim?" -> PATCH /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}
- "Update a resourceclaim?" -> PUT /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}
- "List all status?" -> GET /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaims/{name}/status
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates
- "Create a resourceclaimtemplate?" -> POST /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates
- "Delete a resourceclaimtemplate?" -> DELETE /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Get resourceclaimtemplate details?" -> GET /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Partially update a resourceclaimtemplate?" -> PATCH /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name}
- "Update a resourceclaimtemplate?" -> PUT /apis/resource.k8s.io/v1beta2/namespaces/{namespace}/resourceclaimtemplates/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta2/resourceclaims
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta2/resourceclaimtemplates
- "List all resourceslices?" -> GET /apis/resource.k8s.io/v1beta2/resourceslices
- "Create a resourceslice?" -> POST /apis/resource.k8s.io/v1beta2/resourceslices
- "Delete a resourceslice?" -> DELETE /apis/resource.k8s.io/v1beta2/resourceslices/{name}
- "Get resourceslice details?" -> GET /apis/resource.k8s.io/v1beta2/resourceslices/{name}
- "Partially update a resourceslice?" -> PATCH /apis/resource.k8s.io/v1beta2/resourceslices/{name}
- "Update a resourceslice?" -> PUT /apis/resource.k8s.io/v1beta2/resourceslices/{name}
- "List all deviceclasses?" -> GET /apis/resource.k8s.io/v1beta2/watch/deviceclasses
- "Get deviceclass details?" -> GET /apis/resource.k8s.io/v1beta2/watch/deviceclasses/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaims
- "Get resourceclaim details?" -> GET /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaims/{name}
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaimtemplates
- "Get resourceclaimtemplate details?" -> GET /apis/resource.k8s.io/v1beta2/watch/namespaces/{namespace}/resourceclaimtemplates/{name}
- "List all resourceclaims?" -> GET /apis/resource.k8s.io/v1beta2/watch/resourceclaims
- "List all resourceclaimtemplates?" -> GET /apis/resource.k8s.io/v1beta2/watch/resourceclaimtemplates
- "List all resourceslices?" -> GET /apis/resource.k8s.io/v1beta2/watch/resourceslices
- "Get resourceslice details?" -> GET /apis/resource.k8s.io/v1beta2/watch/resourceslices/{name}
- "List all scheduling.k8s.io?" -> GET /apis/scheduling.k8s.io/
- "List all scheduling.k8s.io?" -> GET /apis/scheduling.k8s.io/v1/
- "List all priorityclasses?" -> GET /apis/scheduling.k8s.io/v1/priorityclasses
- "Create a priorityclass?" -> POST /apis/scheduling.k8s.io/v1/priorityclasses
- "Delete a priorityclass?" -> DELETE /apis/scheduling.k8s.io/v1/priorityclasses/{name}
- "Get priorityclass details?" -> GET /apis/scheduling.k8s.io/v1/priorityclasses/{name}
- "Partially update a priorityclass?" -> PATCH /apis/scheduling.k8s.io/v1/priorityclasses/{name}
- "Update a priorityclass?" -> PUT /apis/scheduling.k8s.io/v1/priorityclasses/{name}
- "List all priorityclasses?" -> GET /apis/scheduling.k8s.io/v1/watch/priorityclasses
- "Get priorityclass details?" -> GET /apis/scheduling.k8s.io/v1/watch/priorityclasses/{name}
- "List all v1alpha1?" -> GET /apis/scheduling.k8s.io/v1alpha1/
- "List all workloads?" -> GET /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads
- "Create a workload?" -> POST /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads
- "Delete a workload?" -> DELETE /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name}
- "Get workload details?" -> GET /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name}
- "Partially update a workload?" -> PATCH /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name}
- "Update a workload?" -> PUT /apis/scheduling.k8s.io/v1alpha1/namespaces/{namespace}/workloads/{name}
- "List all workloads?" -> GET /apis/scheduling.k8s.io/v1alpha1/watch/namespaces/{namespace}/workloads
- "Get workload details?" -> GET /apis/scheduling.k8s.io/v1alpha1/watch/namespaces/{namespace}/workloads/{name}
- "List all workloads?" -> GET /apis/scheduling.k8s.io/v1alpha1/watch/workloads
- "List all workloads?" -> GET /apis/scheduling.k8s.io/v1alpha1/workloads
- "List all storage.k8s.io?" -> GET /apis/storage.k8s.io/
- "List all storage.k8s.io?" -> GET /apis/storage.k8s.io/v1/
- "List all csidrivers?" -> GET /apis/storage.k8s.io/v1/csidrivers
- "Create a csidriver?" -> POST /apis/storage.k8s.io/v1/csidrivers
- "Delete a csidriver?" -> DELETE /apis/storage.k8s.io/v1/csidrivers/{name}
- "Get csidriver details?" -> GET /apis/storage.k8s.io/v1/csidrivers/{name}
- "Partially update a csidriver?" -> PATCH /apis/storage.k8s.io/v1/csidrivers/{name}
- "Update a csidriver?" -> PUT /apis/storage.k8s.io/v1/csidrivers/{name}
- "List all csinodes?" -> GET /apis/storage.k8s.io/v1/csinodes
- "Create a csinode?" -> POST /apis/storage.k8s.io/v1/csinodes
- "Delete a csinode?" -> DELETE /apis/storage.k8s.io/v1/csinodes/{name}
- "Get csinode details?" -> GET /apis/storage.k8s.io/v1/csinodes/{name}
- "Partially update a csinode?" -> PATCH /apis/storage.k8s.io/v1/csinodes/{name}
- "Update a csinode?" -> PUT /apis/storage.k8s.io/v1/csinodes/{name}
- "List all csistoragecapacities?" -> GET /apis/storage.k8s.io/v1/csistoragecapacities
- "List all csistoragecapacities?" -> GET /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities
- "Create a csistoragecapacity?" -> POST /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities
- "Delete a csistoragecapacity?" -> DELETE /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name}
- "Get csistoragecapacity details?" -> GET /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name}
- "Partially update a csistoragecapacity?" -> PATCH /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name}
- "Update a csistoragecapacity?" -> PUT /apis/storage.k8s.io/v1/namespaces/{namespace}/csistoragecapacities/{name}
- "List all storageclasses?" -> GET /apis/storage.k8s.io/v1/storageclasses
- "Create a storageclass?" -> POST /apis/storage.k8s.io/v1/storageclasses
- "Delete a storageclass?" -> DELETE /apis/storage.k8s.io/v1/storageclasses/{name}
- "Get storageclass details?" -> GET /apis/storage.k8s.io/v1/storageclasses/{name}
- "Partially update a storageclass?" -> PATCH /apis/storage.k8s.io/v1/storageclasses/{name}
- "Update a storageclass?" -> PUT /apis/storage.k8s.io/v1/storageclasses/{name}
- "List all volumeattachments?" -> GET /apis/storage.k8s.io/v1/volumeattachments
- "Create a volumeattachment?" -> POST /apis/storage.k8s.io/v1/volumeattachments
- "Delete a volumeattachment?" -> DELETE /apis/storage.k8s.io/v1/volumeattachments/{name}
- "Get volumeattachment details?" -> GET /apis/storage.k8s.io/v1/volumeattachments/{name}
- "Partially update a volumeattachment?" -> PATCH /apis/storage.k8s.io/v1/volumeattachments/{name}
- "Update a volumeattachment?" -> PUT /apis/storage.k8s.io/v1/volumeattachments/{name}
- "List all status?" -> GET /apis/storage.k8s.io/v1/volumeattachments/{name}/status
- "List all volumeattributesclasses?" -> GET /apis/storage.k8s.io/v1/volumeattributesclasses
- "Create a volumeattributesclass?" -> POST /apis/storage.k8s.io/v1/volumeattributesclasses
- "Delete a volumeattributesclass?" -> DELETE /apis/storage.k8s.io/v1/volumeattributesclasses/{name}
- "Get volumeattributesclass details?" -> GET /apis/storage.k8s.io/v1/volumeattributesclasses/{name}
- "Partially update a volumeattributesclass?" -> PATCH /apis/storage.k8s.io/v1/volumeattributesclasses/{name}
- "Update a volumeattributesclass?" -> PUT /apis/storage.k8s.io/v1/volumeattributesclasses/{name}
- "List all csidrivers?" -> GET /apis/storage.k8s.io/v1/watch/csidrivers
- "Get csidriver details?" -> GET /apis/storage.k8s.io/v1/watch/csidrivers/{name}
- "List all csinodes?" -> GET /apis/storage.k8s.io/v1/watch/csinodes
- "Get csinode details?" -> GET /apis/storage.k8s.io/v1/watch/csinodes/{name}
- "List all csistoragecapacities?" -> GET /apis/storage.k8s.io/v1/watch/csistoragecapacities
- "List all csistoragecapacities?" -> GET /apis/storage.k8s.io/v1/watch/namespaces/{namespace}/csistoragecapacities
- "Get csistoragecapacity details?" -> GET /apis/storage.k8s.io/v1/watch/namespaces/{namespace}/csistoragecapacities/{name}
- "List all storageclasses?" -> GET /apis/storage.k8s.io/v1/watch/storageclasses
- "Get storageclass details?" -> GET /apis/storage.k8s.io/v1/watch/storageclasses/{name}
- "List all volumeattachments?" -> GET /apis/storage.k8s.io/v1/watch/volumeattachments
- "Get volumeattachment details?" -> GET /apis/storage.k8s.io/v1/watch/volumeattachments/{name}
- "List all volumeattributesclasses?" -> GET /apis/storage.k8s.io/v1/watch/volumeattributesclasses
- "Get volumeattributesclass details?" -> GET /apis/storage.k8s.io/v1/watch/volumeattributesclasses/{name}
- "List all v1beta1?" -> GET /apis/storage.k8s.io/v1beta1/
- "List all volumeattributesclasses?" -> GET /apis/storage.k8s.io/v1beta1/volumeattributesclasses
- "Create a volumeattributesclass?" -> POST /apis/storage.k8s.io/v1beta1/volumeattributesclasses
- "Delete a volumeattributesclass?" -> DELETE /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name}
- "Get volumeattributesclass details?" -> GET /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name}
- "Partially update a volumeattributesclass?" -> PATCH /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name}
- "Update a volumeattributesclass?" -> PUT /apis/storage.k8s.io/v1beta1/volumeattributesclasses/{name}
- "List all volumeattributesclasses?" -> GET /apis/storage.k8s.io/v1beta1/watch/volumeattributesclasses
- "Get volumeattributesclass details?" -> GET /apis/storage.k8s.io/v1beta1/watch/volumeattributesclasses/{name}
- "List all storagemigration.k8s.io?" -> GET /apis/storagemigration.k8s.io/
- "List all v1beta1?" -> GET /apis/storagemigration.k8s.io/v1beta1/
- "List all storageversionmigrations?" -> GET /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations
- "Create a storageversionmigration?" -> POST /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations
- "Delete a storageversionmigration?" -> DELETE /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}
- "Get storageversionmigration details?" -> GET /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}
- "Partially update a storageversionmigration?" -> PATCH /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}
- "Update a storageversionmigration?" -> PUT /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}
- "List all status?" -> GET /apis/storagemigration.k8s.io/v1beta1/storageversionmigrations/{name}/status
- "List all storageversionmigrations?" -> GET /apis/storagemigration.k8s.io/v1beta1/watch/storageversionmigrations
- "Get storageversionmigration details?" -> GET /apis/storagemigration.k8s.io/v1beta1/watch/storageversionmigrations/{name}
- "List all logs?" -> GET /logs/
- "Get log details?" -> GET /logs/{logpath}
- "List all jwks?" -> GET /openid/v1/jwks/
- "List all version?" -> GET /version/
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
