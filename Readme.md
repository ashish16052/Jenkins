# Installation
1. Build the Jenkins BlueOcean Docker Image
``` 
docker build -t myjenkins .
```

2. Create the network 'jenkins'
``` 
docker network create jenkins
```

# Run the Container
```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8000:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins
```

Connect to jenkins ```https://localhost:8000/ ```

# Get the password
```
docker exec jenkins-blueocean cat var/jenkins_home/secrets/initialAdminPassword
```

# Accessing jenkins workspaces
```
docker exec -it jenkins-blueocean bash
cd /var/jenkins_home/workspace
```

# alpine/socat container to forward traffic from Jenkins to Docker Desktop on Host Machine
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock

docker inspect <container_id> | grep IPAddress
```