This has been adapted from rook-ceph.


The Rook Operator has been installed. Check its status by running:
  kubectl --namespace {{ .Release.Namespace }} get pods -l "app=rook-ceph-operator"

Visit https://rook.io/docs/rook/master for instructions on how to create and configure Rook clusters

Note: You cannot just create a CephCluster resource, you need to also create a namespace and
install suitable RBAC roles and role bindings for the cluster. The Rook Operator will not do
this for you. Sample CephCluster manifest templates that include RBAC resources are available:

- https://rook.github.io/docs/rook/master/ceph-quickstart.html
- https://github.com/rook/rook/blob/master/cluster/examples/kubernetes/ceph/cluster.yaml

Important Notes:
- The links above are for the unreleased master version, if you deploy a different release you must find matching manifests.
- You must customise the 'CephCluster' resource at the bottom of the sample manifests to met your situation.
- Each CephCluster must be deployed to its own namespace, the samples use `rook-ceph` for the cluster.
- The sample manifests assume you also installed the rook-ceph operator in the `rook-ceph` namespace.
- The helm chart includes all the RBAC required to create a CephCluster CRD in the same namespace.
- Any disk devices you add to the cluster in the 'CephCluster' must be empty (no filesystem and no partitions).
- In the 'CephCluster' you must refer to disk devices by their '/dev/something' name, e.g. 'sdb' or 'xvde'.