# Kimai-k8s
**KIMAI App Deployment on Kubernetes**

**•	Kubernetes Cluster setup info: **

o	kubeadm 1.21

o	1 Control Plane Node (Master)

o	1 Worker Node

o	OS: Ubuntu 18.04

o	AWS EC2 instance type: t3.medium

o	Kimai App Containers will run on Kubernetes and Database is running on AWS RDS.

 ![image](https://user-images.githubusercontent.com/25103050/117771158-6fa44b80-b253-11eb-8b6d-bf8b0a020d63.png)

•	Below are Kubernetes manifest files to deploy “KIMAI App” on kubernetes cluster.
 ![image](https://user-images.githubusercontent.com/25103050/117771168-7337d280-b253-11eb-98ce-3881196db6e8.png)

•	**Database:** AWS RDS Mysql Server and create database having name “kimai”.
 ![image](https://user-images.githubusercontent.com/25103050/117771202-7c28a400-b253-11eb-8752-826bf2f7fc0b.png)

•	Kimai App Containers requires some input parameters as environment variables i.e. ADMINMAIL, ADMINPASS, DATABASE_URL and TRUSTED_HOSTS. For the same, Please create configmap and secret object to store these environment variables values. Which can be used in deployments.yaml file for the KIMAI APP Deployment.
 ![image](https://user-images.githubusercontent.com/25103050/117771213-7fbc2b00-b253-11eb-8de6-8ca790a3f1d0.png)

•	To deploy the application on kubernetes cluster fire below command which will create deployment and expose these deployment using service.
 
![image](https://user-images.githubusercontent.com/25103050/117771234-834fb200-b253-11eb-9010-6718159f1fea.png)

•	Below command is used to see logs inside kimai-app pods:
o	Kubectl logs deployment/kimai-deployment
 ![image](https://user-images.githubusercontent.com/25103050/117771246-864aa280-b253-11eb-9bd9-755ba0d03763.png)

•	Kimai-app pods are expose using nodeport service so below command will give us a nodeport.
 ![image](https://user-images.githubusercontent.com/25103050/117771318-98c4dc00-b253-11eb-98db-39760921cb72.png)


•	To access the application visit** NodeIP:NodePort using browser** and check whether your application is running or not.
 ![image](https://user-images.githubusercontent.com/25103050/117771327-9bbfcc80-b253-11eb-9d47-88b61fbbea73.png)

•	Login to application using admin username and password which was defined in kimai-secrets.yaml while deployment:
 ![image](https://user-images.githubusercontent.com/25103050/117771344-9f535380-b253-11eb-94e2-a85ff1d546e5.png)

•	**Areas of optimization:**
o	We can use AWS ECS service to host this application which is cost-effective solution since AWS Provides ECS Master free of cost.
o	We can use AWS EKS for the kubernetes cluster deployment.
o	We can use Terraform to provision the infrastructure.
o	If we are using AWS EKS, we can use AWS ALB as ingress-controller and application pods will be exposed using ingress and ingress-controller (AWS ALB).
o	Since “KIMAI-APP” is PHP application, if it requires continuous read/write operation on file system, we can use AWS EFS and mount Application file system on AWS EFS using Persistent-Volumes and Persistent-Volume-claims.
o	We can also use helm-charts for the deployment


