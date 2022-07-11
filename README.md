# SRE Engineer Interview Exercise

## Exercise 1: Programming

Duration: You should spend around 2 hours

Challenge: Create a prototype of a REST API that generates secure passwords. You can use programming language and libraries of your choice. As input parameters in the request the user has to provide:
* minimum length 
* number of special characters in the password
* number of numbers in the password
* number of passwords that must be created. 

The program must generate the passwords in response and return them in an array.

### Extra Credits
Prepare a minimal setup to deploy your application into a kubernetes cluster.

ANSWER:

- we should create deployment for this pod, then ingress role to expose.
- using node port (not recommended but it's for test purpose)

**NOTE**: When you are ready you can send the results in a public git repo back to us.

## Exercise 2: Infrastructure

Duration: You should spend around 1 hour

### Scenario

In this exercise, Cognigy has two environments, dev and prod, both running on AWS. On each environment, we want to deploy a Kubernetes cluster. Thus, the SRE team prepares Terraform code to manage the infrastructure as code. You find it in this repository in two directories: `dev-environment` and `prod-environment`.

Before answering the questions, please note that:

- You don't need to be familiar with Terraform or AWS to do the exercise. We want to see your knowledge about infrastructure as code, networking and security and more.
- You don't need to run this code. We are even not sure if the code is functional :)
- There are no wrong or right answers.  We want to discuss your solution with you in the interview.

### Questions

1. Please list all the possible improvements to this Terraform code. It can be but NOT limited to code structure, code management, Terraform  syntax, AWS usage, security, Kubernetes.


Answers:

regarding the structure:
- i will define  a seperate file for each componenent: 
for network part: i will put one network.tf file to create (VPC, private subnets, external load balancers in public subnets, security groups and Routing Tables, Nat GWs in Public subnet)
- for EKS cluster do the same, but put NODE group in Autoscaling group.
- Create Bastion Hosts to only have access to your Master nodes.
- define the security group to accept requests from specific SGs.
-  from the file structure i can see two files for terraform code, One for PROD-end and other one for Dev-stage. however it should be one terrafrom code file and i can decide which place to deploy based on my Variables file.
 


2. Design monitoring, logging and alerting architecture for these environments. Y

Answers:

- for monitoring will deploy Promethues and Grafana.
- i will create Promethues Exporters as Pods to collect Data from Kuberentes
- for logging, i will deploy centralized ELK.
- Run Logstash as Pod on Kubenertes cluster to collect metrics from Other pods.

referred. You don't need to write any code here.

### Extra Credit Question

1. Imagine Cognigy grows fast, and you need to scale such environments to dozens of installations. What would be
your suggestion to improve previous solutions to make deployment, monitoring and logging architectures scalable?

Answers:

- install promethues for each environment.
- install Grafana one time to vizualize data from different Promethues servers.
- Alert manager ( Highly available) 
- for ELK, we can use opensearch from AWS, for opensearch i should provision dedicated master.
- for Kuberentes cluster shoulld be dedicated master.
- should use ingress and external Load balancer.
- For deployment, I can use Argo CD. So that every app's helm chart will be hosted on github.
- Use Pod Auto scaler based on Cpu and Load.




























































































































