# Kubernetes Horizontal Pod Autoscaling (HPA) on AWS EKS 🚀

## 📌 Project Overview

This project demonstrates the implementation of **Horizontal Pod Autoscaling (HPA)** in Kubernetes using AWS EKS.

The objective is to understand how Kubernetes automatically scales application pods based on CPU utilization when application traffic increases.

A web application is deployed inside Kubernetes, exposed through an AWS LoadBalancer, and subjected to simulated traffic using a Bash script with parallel HTTP requests.

## 🏗️ Architecture

```text
              User / Client
                   |
                   |
             HTTP Requests
                   |
                   v
           AWS LoadBalancer
                   |
                   v
           Kubernetes Service
                   |
                   v
          Kubernetes Deployment
                   |
          +--------+--------+
          |        |        |
        Pod 1    Pod 2    Pod 3 ...
          |        |        |
          +--------+--------+
                   |
                   v
          Horizontal Pod Autoscaler
                   |
             CPU Monitoring
                   |
          Scale Out / Scale In
```

## 🛠️ Technologies Used

- **AWS EKS** – Managed Kubernetes service
- **Kubernetes** – Container orchestration
- **HPA** – Automatic pod scaling
- **Apache HTTP Server** – Web application container (`httpd`)
- **AWS LoadBalancer** – External application access
- **Bash & cURL** – Traffic generation

## 📂 Project Structure

```text
kubernetes-hpa-autoscaling/
│
├── deployment.yml    # Application deployment
├── service.yml       # LoadBalancer service
├── hpa.yml           # Horizontal Pod Autoscaler configuration
├── test.sh           # Traffic generation script
└── README.md         # Project documentation
```

## ⚙️ Implementation Steps

### 1. Deploy the application

Create a Kubernetes Deployment with CPU resource requests.

```bash
kubectl apply -f deployment.yml
```

Verify the deployment:

```bash
kubectl get deployments
kubectl get pods
```

### 2. Expose the application

Create a LoadBalancer service to expose the application externally.

```bash
kubectl apply -f service.yml
```

Check the LoadBalancer endpoint:

```bash
kubectl get svc
```

### 3. Configure Horizontal Pod Autoscaler

Apply the HPA configuration to automatically adjust the number of application pods based on CPU utilization.

```bash
kubectl apply -f hpa.yml
```

Verify HPA:

```bash
kubectl get hpa
```

### 4. Generate application traffic

Execute the Bash script to generate concurrent HTTP requests against the LoadBalancer endpoint.

```bash
chmod +x test.sh
./test.sh
```

### 5. Monitor autoscaling

Observe the HPA behavior in real time:

```bash
kubectl get hpa -w
```

Monitor pod creation and scaling:

```bash
kubectl get pods -w
```

Check CPU utilization:

```bash
kubectl top pods
```

## 🎯 Key Learning Outcomes

- Understanding Kubernetes Horizontal Pod Autoscaling.
- Configuring CPU resource requests for containers.
- Exposing Kubernetes applications using AWS LoadBalancer.
- Understanding how CPU utilization influences pod scaling.
- Generating concurrent HTTP traffic using Bash and cURL.
- Monitoring Kubernetes workloads and autoscaling behavior.

## 📚 Key Concepts

**Horizontal Scaling:** Increasing or decreasing the number of application pod replicas based on workload demand.

**HPA:** Kubernetes controller that automatically adjusts the replica count of a Deployment or ReplicaSet based on observed metrics.

**CPU Requests:** The CPU resources requested by a container, which are used as the baseline for calculating CPU utilization.

## 👩‍💻 Author
G. Yamini Krishna
Created as part of my hands-on learning journey in AWS, Kubernetes, and Cloud & DevOps engineering.

Always learning, experimenting, and building! 🚀
