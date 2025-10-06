**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks1)

**Author:** Łukasz Brodziak  
**Email:** lukasz.brodziak@gmail.com

---

## Launch a Kubernetes Cluster

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-compute-eks1_e5f6g7h8)

---

## Introducing Today's Project!

In this project, I will setup Kubernetes cluster using Amazon EKS. I will also use tools like eksctl and CloudFormation.

### What is Amazon EKS?

### One thing I didn't expect

### This project took me...

---

## What is Kubernetes?

Kubernetes is a container orchestration platform, which is a fancy way to say that it coordinates containers so they're running smoothly across all your servers. It makes sure all your containers are running where they should, scales containers automatically to meet demand levels, and even restarts containers if something crashes.
It’s THE standard tool for keeping large, container-based applications steady and easy to scale with traffic. That's why big tech companies, startups, and developers worldwide use Kubernetes. Without a tool like Kubernetes, you would create and manage every container manually. You’d have to start each container yourself and keep an eye on them to restart any that crash.
Traffic to your app going up or down would mean turning containers on or off one by one, and you’d also have to make sure each container has access to storage if it needs it. Updating your app would mean carefully swapping out containers without causing downtime.

I used eksctl to create EKS cluster. The create cluster command I ran defined cluster name, node group name, type of EC2 instance, number of nodes to be created at the start, minimum and maximum number of nodes, Kubernetes version to be used and region in which the cluster should be created.

I initially ran into two errors while using eksctl. The first one was because the tool itself was not installed on the EC2 machine. The second one was because of insufficient permissions that the EC2 role had.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-compute-eks1_ff9bfc221)

---

## eksctl and CloudFormation

CloudFormation helped create my EKS cluster by setting up a proper stack with all the resources needed by the EKS cluster. It created VPC resources because the default account VPC needs to be updated manually with all the necessary resources, so it is more convenient to steup a niw VPC already with all the needed resoures.

There was also a second CloudFormation stack for the node group. The difference between a cluster and node group is that cluster is the entire environment the Kubernetes controls. It consists of Control plane and node group which contain the nodes themselves .

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-compute-eks1_w3e4r5t6)

---

## The EKS console

I had to create an IAM access entry in order to view nodes on the cluster. An IAM access entry is like a handshake that connects AWS and Kubernetes. IAM is AWS’s login and permission system, while RBAC (Role Based Access Control) is Kubernetes’s. The entry maps your IAM role to an RBAC role, so the cluster lets you access your nodes. I set it up by going into Access tab and choosing Create in IAM access entries.

It took 20  to create my cluster. Since I'll create this cluster again in the next project of this series, maybe this process could be sped up if I use templates in Terraform or CloudFormation.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-compute-eks1_e5f6g7h8)

---

## EXTRA: Deleting nodes

When you create nodes in a Kubernetes cluster on AWS, each node is actually an EC2 instance!
Kubernetes uses a generic term (node) because different cloud platforms use different cloud resources to be the node; in AWS, we use EC2 instances as our nodes.

Desired size means how many nodes we would like to have in our group. Mininum and maximum sizes are helpful for maintaining high availability in both low and high traffic periods

When I deleted my EC2 instances EKS started recreating them automatically. This is because EKS tries to maintain the desired anount of nodes at all times

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-compute-eks1_q7r8s9t0)

---

---
