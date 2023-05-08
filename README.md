# k8s btfs statefulset

## requirements
This repo is using a EKS and EBS CSI driver for testing
```
# provision a EKS cluster with CSI driver
https://github.com/one2cloudpeter/statefulset_demo#provision-a-eks-cluster-with-csi-driver
```

## steps
```
cd k8s_btfs_statefulset
kubectl apply -f btfs_statefulset.yml
```

check statefulset is being deployed
```
kubectl describe statefulset btfs
```

the pod need arround 2 min to provision successfully, until then the pod will restart mutilple time with an Error.
```
kubectl get pod -w
```

## Error

While the pod pod is restarting and status error, you could get the logs from the pod
```
kubectl logs btfs-0
```

it show the "init settlement err" this error is due to btfs their network connection problems. have to retry a few time, here is the doc for your reference
```
https://github.com/bittorrent/go-btfs/issues/287#:~:text=Or%20you%20can%20retry%20again%20the%20v2.3.0%0AThis%20error%20is%20a%20network%20error.%0A%22init%20settlement%20err%3A%20init%20vault%20service%3A%20vault%20init%3A%20503%20Service%20Temporarily%20Unavailable%22

https://github.com/bittorrent/go-btfs/issues/288#:~:text=this%20error%20is%20caused%20by%20a%20network%20error
```