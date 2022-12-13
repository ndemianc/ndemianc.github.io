---
layout: post
title: Deploying a Rails App with an Nginx Sidecar Container
description:
date: 2019-12-05 15:01:35 +0300
author: sdemian
image: '/images/sdemian-small-image.jpg'
video_embed: https://www.youtube.com/watch?v=XQ5trPfGsA4
tags: [video, aws, sidecar, ecs, deployment]
tags_color: '#618770'
---

> So, You have been working hard on your idea implementation, and now it a time when You first think about deployment of your brand new Ruby on Rails application.

You want to show the world your shinny new website. But there is a problem how to deploy your application, in fault tolerant, resilient and reliable way.

There are already solutions to deployment problem: Heroku, Capistrano, Debian package, etc. You name it,  and Amazon Elastic Container Service.

Amazon Elastic Container Service (Amazon ECS) is a highly scalable, high-performance container orchestration service that supports Docker containers and allows you to easily run and scale containerized applications on AWS. Amazon ECS eliminates the need for you to install and operate your own container orchestration software, manage and scale a cluster of virtual machines, or schedule containers on those virtual machines. Instead, Amazon ECS helps you run microservice applications with native integration to AWS services and enables continuous integration and continuous deployment (CICD) pipelines.

Today we will take a look at Sidecar pattern and how to use Sidecar pattern to deploy application on the AWS cluster using Amazon Elastic Container Service and Amazon Elastic Container Registry.
