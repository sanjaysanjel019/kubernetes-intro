###  First Lab 


***Note:*** This application is based on K8s YT course by [Techworld by Nana](https://www.youtube.com/channel/UCdngmbVKX1Tgre699-XLlUA). You can follow her for awesome DevOps related content <3.


What we'll build:
- An application which will have MONGO and MONGO EXPRESS. We'll create the followiwng items:
    - Deployments
    - configMap
    - secrets
    - Internal and External Service for Communications

#### Overview of the application we'll be building
![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b7a17228-7d3e-4f29-b026-0fed2c5344d2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T085837Z&X-Amz-Expires=86400&X-Amz-Signature=28642843bcdc95c8f710d2567538ac8c6d3c05fb3f382caa2ddc65e9d166a52a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b7a17228-7d3e-4f29-b026-0fed2c5344d2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T085837Z&X-Amz-Expires=86400&X-Amz-Signature=28642843bcdc95c8f710d2567538ac8c6d3c05fb3f382caa2ddc65e9d166a52a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/31b83cea-c96d-42e0-a7e7-8a6a813edd17/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T085908Z&X-Amz-Expires=86400&X-Amz-Signature=82243722b40de708ca0d77548c5a4eaac3f1b9b37236099bcddc23f1b2214c2f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/31b83cea-c96d-42e0-a7e7-8a6a813edd17/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T085908Z&X-Amz-Expires=86400&X-Amz-Signature=82243722b40de708ca0d77548c5a4eaac3f1b9b37236099bcddc23f1b2214c2f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### Creating a service
We'll be using the following YAML file for our configuration for creating our internal service.It is included on the same deployment file as mongo and is separated by three dashes . —-

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
spec:
  selector:
    app: mongodb
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
```

The following is the description  of the YAML file above.
![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/47bb48a4-44e0-452a-a036-54769e1a10db/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T090033Z&X-Amz-Expires=86400&X-Amz-Signature=f27ea55644f9c4bc3a2b5ef03573fb1348268f07d81686172eed16ef0a343936&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/47bb48a4-44e0-452a-a036-54769e1a10db/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T090033Z&X-Amz-Expires=86400&X-Amz-Signature=f27ea55644f9c4bc3a2b5ef03573fb1348268f07d81686172eed16ef0a343936&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)


Before we created a deployment of mongo and had value of containerPort as 27017. So, the tagetPort on our service file has to be same as containerPort as they need to communicate to each other.

The port is the service port.

### **Checking if a service is attached to a correct pod**

To do this we first describe our created service, which in our case is mongodb-service.

```yaml
kubectl describe service mongodb-service
```

The following result will be obtained:

![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/52ed1779-b0c7-4522-b803-db1f93b6bd92/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T090114Z&X-Amz-Expires=86400&X-Amz-Signature=0fc09dcd4c80cf9ee215c75fb83491cb79a31da317c29f2ad14283d99f628679&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/52ed1779-b0c7-4522-b803-db1f93b6bd92/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T090114Z&X-Amz-Expires=86400&X-Amz-Signature=0fc09dcd4c80cf9ee215c75fb83491cb79a31da317c29f2ad14283d99f628679&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

As we see here, we see the endpoint which has an IP and a port. the IP is the IP of the pod  it should attach to. So, we then  have to see the IP of the pod on which this service is running. If the IP of the POD matches the Endpoint of the service file, we are good to go.

To get the IP of the pod we can simply use:

```yaml
kubectl get pod -o wide
```

For a single pod, we get the following result.

![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1b175021-86a7-4f06-af6d-612e5b000a35/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T090134Z&X-Amz-Expires=86400&X-Amz-Signature=31e243fc1ad42aebd6f1dc2a11069fd763c63457a1cf18e1134544e8853b25f4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1b175021-86a7-4f06-af6d-612e5b000a35/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210423%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210423T090134Z&X-Amz-Expires=86400&X-Amz-Signature=31e243fc1ad42aebd6f1dc2a11069fd763c63457a1cf18e1134544e8853b25f4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

As we see here, the IP matches the IP we got above. It means the service is running on the pod we want.