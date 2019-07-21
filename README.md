#B1: Create Cluster
### Kubernetes Engine >
(console.cloud.google.com/kubernetes/list)

#B2: Connect Cluster
### Kubernetes Engine > Cluster >
1. Click "Connect", "Run in Cloud Shell", 
2. In Shell: Enter

#B3: Clone source from GIT
1. In Shell: "ssh-keygen" to see dir of .pub file
2. In Shell: "cat /home/hieuthien95/.ssh/id_rsa.pub" to view public key
3. Copy public key and paste to https://gitlab.com/profile/keys 
(like: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDOdXxNP/qVSj2MoCDNdrGTGtC+vgPznKH8ZwSlkL/rDj4jz5u2yAgF5iUBTS8KxytRka6q5rLNTLicwCngmvHuPAA7FRKSXXYhmQ/vGv/yoaxt/E9SC4sHiwRBlVvXfxXUr2Y1A
9LEbnJeon8A3+l7NqJzmz3hRq9EkJmvh6ZHBxoyhF11XuZyLaQcqu3KDQCRk9xDKo6Dv7WGbsipeQXEAzZah+PYcue0XyiiBNJ+4IkMMkTQJy75LAJRBigdTmfOVf1IozZJeZH6H97mmgFZV0aIKdZuiVxKBMtjRXNe5FrtQvIULP
XVosurONy7fjaNI2GH7inTr2RM5epkyIX1 hieuthien95@cs-6000-devshell-vm-fe8dcc7c-daed-4923-8c55-07b425194155)

5. In Shell: "git clone git@gitlab.com:lak8s/thienbh-lession2.git" to clone src

# B4: Run this Cloned source
1. In Shell: "chmod +x batch.sh", "./batch.sh" to run script in batch.sh
(if just wait to build img: "docker build -t gcr.io/${PROJECT_ID}/golang_health_image:v1 .", not action Step 2)
2. In Shell: "docker ps" to see container is running, "curl localhost:9092/healthcheck" to check api

# B4: Upload the image to a registry
1. In Shell: 
