# multi-container-deployment-k8s
To build and deploy a multi-tier web application using Kubernetes and Docker. Components include: A single-instance Redis to store guestbook entries, Multiple web frontend instances

## Running the app (Kubernetes Cluster)
- Set up an Ingress controller in Docker Desktop environment on a Mac
``
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.0/deploy/static/provider/cloud/deploy.yaml
$ kubectl apply -f ingress.yaml
```

- Apply configurations to run in local environment (I am using Docker Desktop on my Mac)
```
$ kubectl apply -f k8s-config
```

- Start the  app using port forwarding
```
kubectl port-forward svc/frontend 8080:80
```

<img width="991" alt="image" src="https://github.com/Mbaoma/fastAPI/assets/49791498/6f8e7492-ceab-4559-a286-b4f4ae1711bc">

<img width="832" alt="image" src="https://github.com/Mbaoma/fastAPI/assets/49791498/1c0cb7f1-dd0e-4c7d-b757-3b6ef45ff608">

<img width="684" alt="image" src="https://github.com/Mbaoma/multi-container-deployment-k8s/assets/49791498/f2c7a60b-affe-4748-bfde-328939c6804b">


*[Reference](https://kubernetes.io/docs/tutorials/stateless-application/guestbook/)*

## Scaling the App
- Scale Up
```
$ kubectl scale deployment frontend --replicas=3
$ kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
frontend-697bd54cd4-2f84d         1/1     Running   0          47s
frontend-697bd54cd4-7dfph         1/1     Running   1          5d20h
frontend-697bd54cd4-d2k48         1/1     Running   0          47s
redis-follower-6f6cd6cbdb-n7flq   1/1     Running   1          5d20h
redis-leader-58b566dc8b-2fvtd     1/1     Running   1          5d20h
```

- Scale Down
```
$ kubectl scale deployment frontend --replicas=1
$ kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
frontend-697bd54cd4-7dfph         1/1     Running   1          5d20h
redis-follower-6f6cd6cbdb-n7flq   1/1     Running   1          5d20h
redis-leader-58b566dc8b-2fvtd     1/1     Running   1          5d20h
```

# Clean up
```
$ kubectl delete deployment -l app=redis
$ kubectl delete service -l app=redis
$ kubectl delete deployment frontend
$ kubectl delete service frontend
```

- Confirm
```
$  kubectl get pods
$ kubectl get service
```

##  Deploying on Google Kubernetes Engine (GKE)

*[Reference](https://cloud.google.com/kubernetes-engine/docs/tutorials/guestbook)*