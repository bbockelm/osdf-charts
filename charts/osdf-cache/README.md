osdf-cache
==========

The `osdf-cache` Helm chart provides an installation of the
Open Science Data Federation (OSDF) cache; for more information
on the OSDF, read the [OSG documentation overview](https://osg-htc.org/docs/data/stashcache/overview/).

Quick Install
-------------

```
$ helm install osg-htc/osdf-cache
```

Prerequisites
-------------

To run the `osdf-cache` application, you will need:

- Helm 3
- Kubernetes 1.21+
- A persistent storage mountpoint to cache files; either a `hostPath` or a PVC usable.

Installing the Chart
--------------------

Add the OSG Helm repository:

```
$ helm repo add osg-htc https://hub.opensciencegrid.org/opensciencegrid
```

To install the chart with the release name `my-release` in the `osg` namespace:

```
$ helm install my-release osg-htc/osdf-cache -n osg
```

Uninstalling the Chart
----------------------

To uninstall/delete the `my-release` deployment:

```
$ helm delete my-release
```

Configuration
-------------

The following table lists the configurable parameters of the `osdf-cache` chart and their default values.

| Parameter                        | Description                                                                 | Default            |
| :------------------------------- | :-------------------------------------------------------------------------- | :----------------- |
| dataVolumes                      | A list of the data volumes to mount in the cache; each data volume is a dictionary containing either a `claimName` or a `hostPath` name. | (empty; mandatory) |
| metadataVolumes                  | A list of volumes to use for metadata; format is identical to `dataVolumes` | (empty; mandatory) |
| namespaceVolume                  | A dictionary of volumes to use for namespace information.                   | `{}`               |
| logVolume                        | A dictionary of volumes to use for XRootD logs.                             | `{}`               |
| topologyResourceName             | The registered resource name for the instance in OSG topology               | (empty; mandatory) |
| topologyFQDN                     | The registered hostname for the instance in OSG topology                    | (empty; mandatory) |
| hostCertKeySecret                | A kubernetes.io/tls secret to use for TLS server connections.               | `null`             |
| xcacheConfig.spaceLowWatermark   | The "low water" mark for space for the `pfc.diskusage` XCache config.       | 0.90               |
| xcacheConfig.spaceHighWatermark  | The "high water" mark for space for the `pfc.diskusage` XCache config.      | 0.95               |
| xcacheConfig.ramSize             | Amount of memory to use for caching objects.                                | 256m               |
| xcacheConfig.blockSize           | Block size for use by cache.                                                | 128k               |
| xcacheConfig.prefetch            | Number of prefetching blocks per open file.                                 | 10                 |
| xcacheConfig.writeQueueMaxBlocks | The 'max blocks' variable in the `pfc.writequeue` XCache config.            | 16                 |
| xcacheConfig.writeQueueThreads   | The 'nthreads' variable in the `pfc.writequeue` XCache config.              | 4                  |
| extraConfig                      | Name of a ConfigMap; will mount the `config` key's value as a XCache config file | `""`          |
| extraEarlyConfig                 | Name of a ConfigMap; will mount the `config` key's value as the first XCache config file | `""`  |
| image.repository                 | Repository and project for the OSDF cache image                             | hub.opensciencegrid.org/opensciencecgrid/stash-cache |
| image.pullPolicy                 | Pull policy for the cache pod.                                              | IfNotPresent       |
| image.tag                        | Image tag to use.                                                           | `""`               |
| imagePullSecrets                 | List of image pull secrets to use.                                          | `[]`               |
| podAnnotations                   | Annotations to add to the cache pod.                                        | `{}`               |
| podSecurityContext               | Security context for the cache pod.                                         | `{}`               |
| securityContext                  | Security context for the cache container.                                   | `{}`               |
| service.type                     | Type of Kubernetes Service to use.                                          | ClusterIP          |
| service.httpPort                 | Port to use for HTTP connectivity.                                          | 8000               |
| service.httpsPort                | Port to use for HTTPS connectivity.                                         | 8443               |
| service.xrootdPort               | Port to use for xrootd protocol connectivity.                               | 1094               |
| service.annotations              | Annotations to add to the Kubernetes Service object.                        | `{}`               |
| resources                        | Resource requests to add to the cache pod.                                  | `{}`               |
| nodeSelector                     | `nodeSelecter` attribute to use on the cache pod.                           | `{}`               |
| tolerations                      | A list of tolerations to add to the cache pod.                              | `[]`               |
| affinity                         | Node affinity for the cache pod.                                            | `{}`               |

