![Kubernetes Logo](https://i.imgur.com/9d6OMsI.png)

## Self Learning Kubernetes Notes

What does this contains? 

* Kubernetes Starter
* Intro
* Learning materials
* minikube demo

### What is Kubernetes?
 
 In simple terms, Kubernetes is a container orchestration tool. It helps in maintaining the containers.

 When we build a containerized application and if there are large number of such containers, we need tool such as Kubernetes that help us to manage those containers and automate our workflow.

 ##### What features does Kubernetes provides?
 - High Availability : The user should not have any downtime.

- Scalability: the application normally have very high response time.

- Disaster Recovery - backup and restore.


#### Kubernetes basic terminologies

1. Pods: Pods are the smallest and the most basic unit in Kubernetes. Each pod get their own IP address so that they can communicate. A pod may be running a service like any application usually within a container.
2. Service: Service is logical set of pods and each pod will have their own service. Lifecycle of Pod and service are not interconnected. Service are generally categorized into:
    - Internal  
    - External
3. Node - A node is a single host in K8s. This is used to run virtual or physical machine. There may be multiple/single pods within a node.
4. ReplicaSet: It is used to identify the particular number of pod replicas running inside a node.
5. ConfigMap : It contains all the external configuration of our application like database URL. The reason we need this is because this acts as a central repo to other components so if we have to make any changes like change in DB_URL we can simply change here and all changees will be reflected back.

#####  ⚠ DO NOT STORE CREDENTIALS ON CONFIGMAP.
6. Secret: As name suggests it stores all the secret info like DB_USERNAME and DB_PASSWORD. We should always store such info in encrypted format rather than plain text.
7. Volumes: This attaches a physical storage to the pod. Data mey be lost while resetting since it is not persistent.
##### ⚠ K8s does not manage data persistence.
8. Deployment: We do not directly create a pod in K8s. We create blueprint of the pod and the rest is handled by K8s. The blueprint for creating pod is called deployment.

### Kubernetes Architecture

The core architecture is that 3 process must be installed on every node. Nodes are cluster service that actually do the work. So, it is also called worker node.

Those three processes are:
- Container Runtime
- Kubelets
- Kube-Proxy


####  Deploying the build images using Kubernetes

We use `kubectl` to deploy our applications, which is a CL Tool to help you interact with Kubernetes.

```yaml
kubectl apply -f deployment.yaml
```

## More commands about K8s

To get the cotainers running on our system:

```jsx
	kubectl get nodes
```

Check the status of the cluster:

```jsx
<cluster-name> status
```

Similarly to get other infos such as pods, services we can do the following. In this case, we're usig a minikube cluster.

```jsx
~~ kubectl get pods
~~ kubectl get services
```

### Creating Kubernetes Components

To create a new component you simply do `kubectl create`:



---

### Creating an NGINX deployment

```jsx
kubectl create deployment nginx-depl --image=nginx

The type is:
kubectl create deployment <deployment-name> --image=<image_you_want>
```

### Editing the configuration file of Deployment

```jsx
kubectl edit deployment <deployment-name>
eg:
kubectl edit deployment nginx-depl
```

### Getting the logs

kubectl logs <pod-name>

—> Getting the description

```jsx
kubectl describe pod <pod-name>
```

Get inside the terminal of the pod:

```jsx
kubectl exec -it <pod-name> -- /bin/bash
```

## Some other important commads

As we see, if we have to create multiple pods with different images, it will be heft to type all those things on CLI. That's why we use `**kubectl apply**` command.

With this, we make a configuration file and pass it as an argument.

```jsx
kubectl apply -f [file-name]
```

 

**RECAP**

![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9ed33eed-97d4-477e-ad13-b5f24bb58f45/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T085524Z&X-Amz-Expires=86400&X-Amz-Signature=ef72779e8e866151859cab004b7b1a39a22295910cdf01e0835a81dc7b95f102&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9ed33eed-97d4-477e-ad13-b5f24bb58f45/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T085524Z&X-Amz-Expires=86400&X-Amz-Signature=ef72779e8e866151859cab004b7b1a39a22295910cdf01e0835a81dc7b95f102&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

