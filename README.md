# multi-container-deployment-k8s

To build and deploy a multi-tier web application using Kubernetes and Docker. Components include: A single-instance Redis to store guestbook entries, Multiple web frontend instances

## Running the app (Kubernetes Cluster)

- Set up an Ingress controller in Docker Desktop environment on a Mac

```
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.0/deploy/static/provider/cloud/deploy.yaml
$ kubectl apply -f ingress.yaml
```

- Apply configurations to run in local environment (I am using Docker Desktop on my Mac)
```
$ kubectl apply -f k8s-config
```

<img width="991" alt="image" src="https://github.com/Mbaoma/fastAPI/assets/49791498/6f8e7492-ceab-4559-a286-b4f4ae1711bc">

<img width="832" alt="image" src="https://github.com/Mbaoma/fastAPI/assets/49791498/1c0cb7f1-dd0e-4c7d-b757-3b6ef45ff608">

*[Reference](https://kubernetes.io/docs/tutorials/stateless-application/guestbook/)*
