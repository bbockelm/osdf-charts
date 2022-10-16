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

| Parameter   | Description                                                          | Default            |
| :---------- | :------------------------------------------------------------------- | :----------------- |
| dataVolumes | A list of the data volumes to mount in the cache; each data volume   | (empty; mandatory) |
|             | is a dictionary containing either a `claimName` or a `hostPath` name
