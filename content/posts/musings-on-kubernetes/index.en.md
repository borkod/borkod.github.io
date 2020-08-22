---
title: "Musings on Kubernetes"
date: 2020-08-19T20:53:21-04:00
draft: false
description : "Recent updates related to Kubernetes"
tags : [
    "Azure",
    "Microsoft",
    "Kubernetes",
    "AKS",
    "Azure Kubernetes Service"
]
author: "Borko"
authorLink: "https://www.b3o.ca"
featuredImage: "featured-image"
featuredImagePreview: "featured-image"
resources:
- name: "featured-image"
  src: "featured-image.jpg"
- name: "featured-image"
  src: "featured-image.jpg"

lightgallery: true

toc:
  auto: false
---
It has been really busy few months! For a long while, I've had a lot of interest in Kubernetes / Docker technologies, and I've always kept an eye on the development in that ecosystem. I've occasionally played around with some of the tooling, but I never had time to really delve deep into it. Over the past few months, there have been some changes in my work and it shifted its focus on Kubernetes technology. I was really excited by the chance to get back to it! The global COVID situation developing around the globe resulted in my summer travel plans being cancelled and extracurricular social activities being significantly reduced. I decided to try and make the best of the situation and took that opportunity to really immerse myself into the Kubernetes technology ecosystem. Over the past few months, I've focused on doing lots of courses, readings, and hands-on work and absorb as much learning as I could. I thought I'd share a few random thoughts/ideas/opinions I've developed as I've been expanding my knowledge and experience with this technology.

## Certifications

Cloud Native Computing Foundation ([CNCF](https://www.cncf.io/)), in collaboration with [The Linux Foundation](https://www.linuxfoundation.org/), offers two certification programs for those looking to validate their Kubernetes knowledge or attain an industry accreditation.

The Certified Kubernetes Administrator ([CKA](https://www.cncf.io/certification/cka/)) program focuses on Kubernetes cluster administration topics with special attention given to cluster installation, configuration and maintenance, networking, security, and troubleshooting.

The Certified Kubernetes Application Developer ([CKAD](https://www.cncf.io/certification/ckad/)) exam places focus on defining Kubernetes resources and primitives related to deploying applications on top of the platform.

After much time and effort preparing, I ended up writing both exams and was successful in obtaining both certifications. In contrast to many certification exams, these tests are all hands-on exercises with no academic or multiple choice questions. Both exams are challenging in their own respect.  Common to both tests is that you're really time constrained. My experience was that the questions need to be completed very quickly in order to finish the exam in alloted time and do well. CKA exam is longer, covers more content and wider range of topics. Additionally, it requires a deeper knowledge and understanding of networking and Linux OS administration. On the other hand, CKAD is easier in a sense that it is shorter and covers less topics. However, it provides less time on per question basis, making it also a challenging test.  Both tests require the candidate to have a very good mastery of the technology to succeed, and thus lot's of preparation.

CNCF recently [announced](https://www.cncf.io/blog/2020/07/15/certified-kubernetes-security-specialist-cks-coming-in-november/) addition of a new Certified Kubernetes Security Specialist (CKS) program. I will be looking to write that exam once the certification becomes generally available in November.

## Training Resources

There are a plethora of resources out there online for tips and guides on preparing for these exams. I will just high-light a couple.

For online training courses, The Linux Foundation offers training courses for both [CKA](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/) and [CKAD](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/). Udemy also has a couple of good courses for those interested in preparing for the exams ([CKA](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/) and [CKAD](https://www.udemy.com/course/certified-kubernetes-application-developer/)). All of these courses provide hands-on exercises for gaining practical familiarity working with Kubernetes. From my experience, I would recommend Udemy courses slightly over the Linux Foundation courses, especially taking into account the price and value.

For exercises, there are a lot of resource to be found online by doing some Google searches. [Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) is the canonical go-to resource for anybody looking to delve deep into cluster administration (and preparing for the CKA exam). I found [this](https://github.com/dgkanatsios/CKAD-exercises) GitHub repo to contain a pretty complete list of review exercises for CKAD exam.

The best and final tip I would offer is to just stand up a Kubernetes cluster and start developing. Hands-on preparation is essential. Practice! Practice! Practice!

## Getting Started

[Installing the kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) command line tool is the first step for working with Kubernetes. 

Azure and AWS cloud providers offer managed Kubernetes services ideal for getting started quickly.

To get started on Azure:
```bash
# Create a resource group
az group create --name <resource group> --location <location>

# Create Azure Kubernetes Cluster
az aks create --resource-group <resource group> --name <AKS Name> --node-count 3

# Get Login Credentials
az aks get-credentials --resource-group <resource group> --name <AKS Name>
```

To get started on AWS:
```bash
eksctl create cluster --name <EKS Name> --version 1.16 --region <AWS region> --nodegroup-name <node group name> --node-type t3.medium --nodes 3 --nodes-min 1 --nodes-max 4 --managed
```

For a local installation, [Minikube](https://kubernetes.io/docs/setup/learning-environment/minikube/) offers an easy and quick way to get started with a learning environment.