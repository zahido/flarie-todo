## Flarie Todo Application Structure Of This Project:

This repository contains the source code for the Flarie Todo application, Dockerfiles, Kubernetes manifests, and CI/CD setup.

```
root_directory
├── flarie-todo
    ├── .github/workflows
    ├── k8s
    ├── spec
    ├── src
    ├── .dockerignore
    ├── .gitignore
    ├── Dockerfile
    ├── package.json
    ├── yarn.lock
    └── readme.md
```

## Docker Image

The Docker image is publicly on Docker Hub:

[ Docker Image: cypher404/flarie-todo ] [ docker pull cypher404/flarie-todo ]

## CI/CD Pipeline

I have deployed a CI/CD pipeline using GitHub Actions. The pipeline automatically builds and deploys the Docker image to Docker Hub whenever changes are pushed to the `main` branch.
You can find the workflow configuration in [ .github/workflows/ci-cd.yml ]

Note: I have removed this line from CI/CD because after finishing the task I have deleted the VM.

      - name: SSH into Azure VM To Deploy to Kubernetes
        uses: appleboy/ssh-action@master
        with:
          host: 20.127.235.98
          username: ${{ secrets.AZURE_VM_USERNAME }}
          password: ${{ secrets.AZURE_VM_SSH_KEY }}
          script: |
           cd flarie-todo
           kubectl apply -f k8s/deployment.yaml
           kubectl apply -f k8s/service.yaml

## Kubernetes Deployment

Kubernetes manifest files:

- [ Deployment Manifest ]  (`k8s/deployment.yaml`)
- [ Service Manifest ]     (`k8s/service.yaml`)

Apply these manifests to deploy the application into a Kubernetes cluster using NodePort service on port 31000.

``NodePort has a default port range from 30000–32767. In the task mentioned port was 34567 which is invalid.``

## Deploy & Run The Project

To run this application locally using Docker, follow these steps:

1. Clone this repository: `git clone https://github.com/zahido/flarie-todo`
2. Run the Docker container: `docker run -p 3000:3000 -itd cypher404/flarie-todo`
4. Access the application: `http://localhost:30000`

To run this dockerized application into a Kubernetes cluster, follow these steps:

1. Kubernetes Cluster: I have installed Minikube in a vm and deploy a cluster.
2. Apply the Kubernetes manifests to your cluster: 'kubectl apply -f deployment.yaml' 'kubectl apply -f service.yaml'
3. Verify that the application is running: 'kubectl get pods' 'kubectl get services'
