# B1: Create Cluster
### Kubernetes Engine >
(console.cloud.google.com/kubernetes/list)


# B2: Connect Cluster
### Kubernetes Engine > Cluster >

1. Click "Connect", "Run in Cloud Shell", 

2. Shell: Enter


# B3: Clone source from GIT
1. See dir of .pub file
```
ssh-keygen
```

2. View public key
```
cat /home/hieuthien95/.ssh/id_rsa.pub
```

3. Copy public key and paste to https://gitlab.com/profile/keys 

(like: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDOdXxNP/qVSj2MoCDNdrGTGtC+vgPznKH8ZwSlkL/rDj4jz5u2yAgF5iUBTS8KxytRka6q5rLNTLicwCngmvHuPAA7FRKSXXYhmQ/vGv/yoaxt/E9SC4sHiwRBlVvXfxXUr2Y1A
9LEbnJeon8A3+l7NqJzmz3hRq9EkJmvh6ZHBxoyhF11XuZyLaQcqu3KDQCRk9xDKo6Dv7WGbsipeQXEAzZah+PYcue0XyiiBNJ+4IkMMkTQJy75LAJRBigdTmfOVf1IozZJeZH6H97mmgFZV0aIKdZuiVxKBMtjRXNe5FrtQvIULP
XVosurONy7fjaNI2GH7inTr2RM5epkyIX1 hieuthien95@cs-6000-devshell-vm-fe8dcc7c-daed-4923-8c55-07b425194155)

5. Clone src from git
```
git clone git@gitlab.com:lak8s/thienbh-lession2.git
```


# B4: Docker
1. create IMG
```
docker build -t gcr.io/${PROJECT_ID}/golang_health_image:v1 .
```

or 

Run script by batch.sh
```
chmod +x batch.sh
./batch.sh
```

2. Test image
```
docker run -d --name golang_health_container -p 9092:9092 golang_health_image
docker ps
curl localhost:9092/healthcheck
```


# B5: Upload the image to a registry
1. Auth
```
gcloud auth configure-docker
```

2. Push this image to repo
```
docker push gcr.io/${PROJECT_ID}/golang_health_image:v1
```

3. Check uploaded images

Container Registry > Images > 

(console.cloud.google.com/gcr)


# B6: Deploy

1. Deploy
```
kubectl run health-check-web --image=gcr.io/iconic-era-243808/golang_health_image:v1 --port 8080
```

Or

Go to: Kubernetes Engine > Workload > , click Deploy

(https://console.cloud.google.com/kubernetes/workload/deploy)

2. Expose IP
```
kubectl expose deployment health-check-web --type=LoadBalancer --port 80 --target-port 8080
```

Or

Go to: Kubernetes Engine > Workload > , click Expose

(https://console.cloud.google.com/kubernetes/workload)
```
---
apiVersion: "v1"
kind: "Service"
metadata:
  name: "health-check-web-service"
  namespace: "default"
  labels:
    run: "health-check-web"
spec:
  ports:
  - protocol: "TCP"
    port: 80
    targetPort: 8080
  selector:
    run: "health-check-web"
  type: "LoadBalancer"
  loadBalancerIP: ""
```

# B7: Deploy new version
```
kubectl set image deployment/health-check-web health-check-web=$IMG_NAME
```

# B8: Check result
```
kubectl get pods
kubectl get service
kubectl scale deployment health-check-web --replicas=3
```

or 

Go to: Kubernetes Engine > Services & Ingress >

(ttps://console.cloud.google.com/kubernetes/discovery)

...

https://cloud.google.com/kubernetes-engine/docs/tutorials/hello-app/

https://cloud.google.com/container-registry/docs/
