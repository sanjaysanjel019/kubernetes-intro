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

