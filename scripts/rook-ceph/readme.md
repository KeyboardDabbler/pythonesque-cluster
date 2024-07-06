
kubectl apply -f ./scripts/rook-ceph/cleanup.yaml

kubectl get jobs

kubectl get pods -l job-name=cleanup-rook-disks

kubectl logs cleanup-rook-disks-r5m5z

kubectl delete -f ./scripts/rook-ceph/cleanup.yaml
