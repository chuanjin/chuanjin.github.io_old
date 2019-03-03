title: Continuous Delivery
date: 2015-10-02 23:34:01
tags: [Tools]
categories: R&D

---
Software development and deployment work flow is quite important for a development team when the product has rapid iterations and code base getting more and more large. There are three concepts/terms around development & deployment: Continuous Integration, Continuous Delivery and Continuous Deployment.

![](/images/pipeline.png)

<!--more-->

# Continuous Integration


Submit changes to mainline to integrate code into a shared repository many times per day. All the tests have to pass locally before check-in and each commit is then verified by an automated CI server, if any test fails,  team members can get notified to detect problems early. By integrating regularly, you can detect errors quickly, and locate them more easily. Therefore, the product can have fast iteration without sacrificing quality. 


# Continuous Delivery 


The natural extension of Continuous Integration. Continuous delivery is a series of practices to ensure that new features or bug fix can be rapidly and safely deployed to production by delivering every change to a production-like environment through rigorous automated testing. Since every change is delivered to a staging environment using complete automation, team can have confidence that the application can be deployed to production with a button push when the business is ready.


# Continuous Deployment


The next step of continuous delivery. Every change that passes the automated tests is deployed to production automatically. 

Continuos Delivery make teams ensure that every change to the system is releasable, and in many cases, it is up to the the business level to make the decision whether or not and when to deploy to production. Check the different between Continuous Delivery and Continuous Deployment below.


![](/images/cd.jpg)
