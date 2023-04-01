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

Connect to jenkins ```https://localhost:8080/ ```

# Get the password
```
docker exec jenkins-blueocean cat var/jenkins_home/secrets/initialAdminPassword
```

# Accessing jenkins workspaces
```
docker exec -it jenkins-blueocean bash
cd /var/jenkins_home/workspace
```