# B1: Create Cluster
### Kubernetes Engine >
(console.cloud.google.com/kubernetes/list)

# B2: Connect Cluster
### Kubernetes Engine > Cluster >

1. Click "Connect", "Run in Cloud Shell", 

2. Shell: Enter

# B3: Clone source from GIT
1. Shell: "ssh-keygen" to see dir of .pub file

2. Shell: "cat /home/hieuthien95/.ssh/id_rsa.pub" to view public key

3. Copy public key and paste to https://gitlab.com/profile/keys 

(like: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDOdXxNP/qVSj2MoCDNdrGTGtC+vgPznKH8ZwSlkL/rDj4jz5u2yAgF5iUBTS8KxytRka6q5rLNTLicwCngmvHuPAA7FRKSXXYhmQ/vGv/yoaxt/E9SC4sHiwRBlVvXfxXUr2Y1A
9LEbnJeon8A3+l7NqJzmz3hRq9EkJmvh6ZHBxoyhF11XuZyLaQcqu3KDQCRk9xDKo6Dv7WGbsipeQXEAzZah+PYcue0XyiiBNJ+4IkMMkTQJy75LAJRBigdTmfOVf1IozZJeZH6H97mmgFZV0aIKdZuiVxKBMtjRXNe5FrtQvIULP
XVosurONy7fjaNI2GH7inTr2RM5epkyIX1 hieuthien95@cs-6000-devshell-vm-fe8dcc7c-daed-4923-8c55-07b425194155)

5. Shell: "git clone git@gitlab.com:lak8s/thienbh-lession2.git" to clone src

# B4: Run this Cloned source
1. Shell: "chmod +x batch.sh", "./batch.sh" to run script in batch.sh

(if just wait to build img: "docker build -t gcr.io/${PROJECT_ID}/golang_health_image:v1 .", not action Step 2)

2. Shell: "docker ps" to see container is running, "curl localhost:9092/healthcheck" to check api

# B5: Upload the image to a registry
1. Shell: "gcloud auth configure-docker"

2. Shell: "docker push gcr.io/${PROJECT_ID}/golang_health_image:v1" to push this image to repo

3. Go to: Container Registry > Images > 

(console.cloud.google.com/gcr)

To see uploaded images

# B6: Deploy

1. Shell: "kubectl run health-check-web --image=gcr.io/iconic-era-243808/golang_health_image:v1 --port 8080" deploy

Or

Go to: Kubernetes Engine > Workload > , click Deploy

(https://console.cloud.google.com/kubernetes/workload/deploy)

2. Shell: "kubectl expose deployment hello-web --type=LoadBalancer --port 80 --target-port 8080"

Or

Go to: Kubernetes Engine > Workload > , click Expose

(https://console.cloud.google.com/kubernetes/workload)

To expose port

3. Port: 80, Target Port: 8080

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

4. Go to: Kubernetes Engine > Services & Ingress >

(ttps://console.cloud.google.com/kubernetes/discovery)

To check result

"kubectl get pods"

"kubectl get service"

"kubectl scale deployment hello-web --replicas=3"

...



https://cloud.google.com/kubernetes-engine/docs/tutorials/hello-app/

https://cloud.google.com/container-registry/docs/
