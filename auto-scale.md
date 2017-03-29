#Auto scale example

1.Create a deployment of some apache containers
```
kubectl run php-apache --image=gcr.io/google_containers/hpa-example --requests=cpu=200m --expose --port=80
```

2.Create a horizontal pod autoscaler
```
kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
```
Check the state
```
kubectl get hpa
```

3. Increase the load
```
kubectl run -i --tty load-generator --image=busybox /bin/sh

while true; do wget -q -O- http://php-apache.default.svc.cluster.local; done
```

check the state
```
kubectl get hpa
kubectl get deployment php-apache
```

4. Stop the load
Abort busybox command
check the state
```
kubectl get hpa
kubectl get deployment php-apache
```


