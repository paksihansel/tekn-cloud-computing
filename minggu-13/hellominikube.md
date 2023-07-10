### Preparation
1. Make sure your pc has installed with minikube and kubectl

### Create a minikube cluster
1. Run this command bellow <br>
![01](img1.png)

### Open the Dashboard
1. Open new terminal and run <br>
![02](img2.png)

### Create a Deployment
1. Use the kubectl create command to create a Deployment that manages a Pod. The Pod runs a Container based on the provided Docker image. <br>
![03](img3.png)
2. View the Deployment: <br>
![04](img4.png)
3. View the Pod: <br>
![05](img5.png)
4. View cluster events:<br>
![06](img6.png)
5. View the kubectl configuration:<br>
![07](img7.png)

### Create a Service
1. Expose the Pod to the public internet using the kubectl expose command: <br>
![08](img8.png)
2. View the Service you created: <br>
![09](img9.png)
3. Run the following command: <br>
![10](img10.png)

### Enable addons
1. List the currently supported addons:
![11](addons-output.png)
2. View the Pod and Service you created by installing that addon:
![12](addons-output.png)

### Clean up
1. Now you can clean up the resources you created in your cluster:
![13](cleanup-kubectl-delete-deploy.png)
2. Stop the Minikube cluster
![14](cleanup-kubectl-stop.png)