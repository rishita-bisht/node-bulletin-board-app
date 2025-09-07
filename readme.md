# Vue Events Bulletin Board

This project is based on the [Vue.js tutorial on Scotch.io](https://scotch.io/tutorials/build-a-single-page-time-tracking-app-with-vue-js-introduction) and the original Vue Events Bulletin Board app. Modifications have been made to enable **Docker containerization** and **Kubernetes deployment on Minikube**.
Learning Outcomes / Key Concepts

Containerization with Docker

1. Learned how to package a Node.js application into a Docker image.

2. Understood the importance of ports, working directories, and imagePullPolicy when deploying to Kubernetes.

3. Local Kubernetes Deployment with Minikube

4. Gained experience creating Deployments and Services in Kubernetes.

5. Learned how to expose a Node.js application through a NodePort service.

6. Practiced troubleshooting pods with ImagePullBackOff and ErrImagePull.

Networking and Port Management

1. Learned that the container port must match the service port.

2. Understood that Node servers must bind to 0.0.0.0 (not localhost) for Kubernetes to route traffic.

Continuous Deployment Workflow

1. Practiced a rebuild → redeploy → restart pod → verify workflow.

2. Learned how to make iterative changes in a local Kubernetes environment without affecting the original project.

3. Debugging & Problem-Solving

Handled common Kubernetes issues:

1. Service unreachable due to no running pods

2. Image not being found locally

3. Terminal “watch” mode for pods

4. Learned to systematically verify image building, pod status, and service exposure.

Versioning & MIT Compliance

1. Learned how to fork a project, make modifications, and maintain MIT license compliance.

2. Learned to credit the original project while adding custom deployment workflows.


## Installation (Local Development)

1. Clone the repository:

```
git clone https://github.com/rishita-bisht/node-bulletin-board-app.git
cd node-bulletin-board-app
```

2. Install dependencies:

```
npm install
```

3. Run the server:

```
node server.js
```

4. Visit in your browser:

```
http://localhost:8080
```

> Make sure `server.js` binds to `0.0.0.0` so it is accessible from Kubernetes pods:

```js
app.listen(8080, '0.0.0.0', () => {
  console.log('Magic happens on port 8080...');
});
```

---

## RESTful API

* Built with Node.js & Express for backend server and router.
* Provides CRUD operations on *events* model.
* Supports Traditional Chinese translations.

### Optional: Go Backend

If you want a Go backend instead, see [thewhitetulip/go-vue-events](https://github.com/thewhitetulip/go-vue-events).

---

## Docker & Kubernetes (Minikube) Deployment

### Docker Build

```
eval $(minikube docker-env)
docker build -t node-bulletin-board-app:latest .
```

### Kubernetes Deployment

1. Apply Deployment and Service:

```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

2. Delete old pods:

```
kubectl delete pod -l app=node-bulletin-board-app
```

3. Watch the pods start:

```
kubectl get pods -w
```

4. Open the app:

```
minikube service node-bulletin-board-app
```

---

### Quick Rebuild & Deploy Workflow

```
eval $(minikube docker-env)
docker build -t node-bulletin-board-app:latest .
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl delete pod -l app=node-bulletin-board-app
minikube service node-bulletin-board-app
```

---

## License

This project includes modifications and is distributed under the **MIT License**.
Original Vue Events Bulletin Board tutorial and code licensed under MIT.

* Original project: [Vue Events Bulletin Board](https://scotch.io/tutorials/build-a-single-page-time-tracking-app-with-vue-js-introduction)
* Your modifications: Docker and Kubernetes deployment instructions


