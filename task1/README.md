# Task1
## Homework
### - Create a deployment nginx. Set up two replicas. Remove one of the pods, see what happens.


1. Create deployment
```
 kubectl create deployment nginx --image=nginx
 ```
 2. Create replica
 ```
  kubectl scale deploy nginx --replicas 2
  ```
  3. View pods and deployment
```
kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
firstcont                1/1     Running   0          40h
nginx-6799fc88d8-8pct6   1/1     Running   0          6m42s
nginx-6799fc88d8-zq99d   1/1     Running   0          9h

kubectl get deploy
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   2/2     2            2           9h
```
4. Delete pod nginx-6799fc88d8-8pct6
```
kubectl delete pod nginx-6799fc88d8-8pct6
pod "nginx-6799fc88d8-8pct6"

kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
firstcont                1/1     Running   0          40h
nginx-6799fc88d8-j9tft   1/1     Running   0          8s
nginx-6799fc88d8-zq99d   1/1     Running   0          9h
```

5. Get port-forward 
```html
kubectl port-forward --address=0.0.0.0  deploy/nginx 7800:80 &

curl 127.0.0.1:7800

Handling connection for 7800
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
Conclusion: K8s create new pod, because replica numbers=2


