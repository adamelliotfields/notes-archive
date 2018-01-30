# Cloud Platform Comparison
> :calendar: *June 25, 2017*

This is a list of the "always free" tiers from major cloud Platform-as-a-Service providers.  

Note that not every feature is included, just the core features:
* Platform-as-a-Service (i.e., Heroku)
* Infrastructure-as-a-Service (i.e., Digital Ocean)
* Database-as-a-Service (i.e., MongoDB Atlas)
* Cloud Storage
* Private Repositories
* Serverless Architecture (see below)

### TLDR
Both Google and Amazon offer a vast array of services to build out incredibly powerful web applications, with the core being a container-based, auto-scaling, load-balanced platform to run your app. On Google this is App Engine Flexible Environment, on Amazon this is Elastic Beanstalk. Both cost over $40/mo with the basic configuration, and can cost more if your app receives thousands of requests simultaneously and needs to spin up new instances to handle the load.  

If you do not need that sort of power, I'd go with Heroku's $7/mo Hobby Plan (which includes managed PostgreSQL).  

For Linux virtual machines, Linode gives you the most bang for your buck for $5/mo (1 core, 1GB RAM, 20GB SSD), however they've had some major issues in the past (user passwords leaked, multiple DDoS attacks as recently as late 2016). For that reason, Digital Ocean seems to be the most recommended.

I'm going to stick with Google Cloud Platform and use their Compute Engine virtual machines. Their web and mobile dashboards are the best, GitHub mirroring works flawlessly, they have really great documentation and tutorials, and with the $300 credit and 1 free VM per month, I can have 6 VMs running with static public IPs that I can SSH into from my computer, Chrome, or their iOS app. Since each Compute Engine has full access to all Google Cloud APIs, I can easily add a Cloud Datastore database or use Cloud Storage buckets for uploading static assets like images.

### Serverless Architecture
This allows you to provide a single function that gets fired when a HTTP event is triggered. The pricing is very simple, you pay for the amount of function calls made, the memory used to execute the function, and the time it took for the function to finish.  

A simple example (taken from Amazon Lambda), to serve an `index.html` file, when a `GET` request is sent to the `/` route:

```
var fs = require('fs');

exports.get = function(event, context) {
  var contents = fs.readFileSync('public/index.html');
  context.succeed({
    statusCode: 200,
    body: contents.toString(),
    headers: {'Content-Type': 'text/html'}
  });
};
```

This function has a memory allocation of 128MB (the lowest). Based on that, it can be called 1 million times per month with a total execution time of 3.2 million seconds and remain in Amazon's free tier. You can also set timeouts to make sure you don't burn through your compute time with an endless loop (default is 3 seconds).

## Google Cloud Platform
Pros:
* Google's dashboard is the easiest to navigate.
* Automated GitHub and Bitbucket mirroring in Cloud Source.
* 1 free Virtual Machine instance (Compute Engine).
* SSH on mobile.
* $300 credit to use within 12 months.

Cons:
* Cloud Shell freezes on me 100% of the time, so I was unable to complete the tutorial.
* I cannot create a Cloud Source repository unless I use GitHub mirroring (I have an open ticket).
* Free tier for App Engine is [Standard Environment](https://cloud.google.com/appengine/docs/standard) only and does not support Node.js.

Sample Pricing:
* Compute Engine (f1-micro): $6/mo (0.2 core, 0.6GB RAM, 10GB SSD)
* Compute Engine (g1-small): $16/mo (0.5 core, 1.7GB RAM, 10GB SSD)
* Compute Engine (custom): $23/mo (1 core, 2GB RAM, 10GB SSD)
* App Engine (Flexible): $44/mo; $0.10/hr (1 instance, 1 core, 1GB RAM, 10GB HDD)

*Every additional 1 GB of memory and 10GB of storage (SSD) is about $2/mo (each) for Compute Engine.*  
*Every additional GB of memory is about $5/mo, and every additional 30GB of storage (HDD) is about $1/mo for App Engine.*

### Google App Engine (Standard)
> Platform for building scalable web applications and mobile backends.
* Java, Python, PHP, or Go runtimes.
* 28 instance hours per day.
* 5GB storage.

### Google Compute Engine
> Scalable, high-performance virtual machines.
* 1 instance per month.
* 30GB HDD.

### Google Cloud Functions
> A serverless environment to build and connect cloud services with code.
* 2,000,000 invocations per month.
* 400,000 GB/s compute time.

### Google Cloud Datastore
> Highly scalable NoSQL database.
* 1GB storage.
* 50,000 reads, 20,000 writes, 20,000 deletes per day.

### Google Cloud Storage
> Best in class performance, reliability, and pricing for your storage needs.
* 5GB-months.
* 5000 Class-A operations per month.
* 50000 Class-B operations per month.

### Google Cloud Source
> Multiple private Git repositories hosted on Google Cloud Platform.
* 1GB private hosting.

## Amazon Web Services
Pros:
* CodeStar provides server provisioning (Lambda, EC2, or EBS), a private repository, CI/CD, and automated deployment all in one.
* Lightsail VMs can access all AWS services through VPC peering.
* [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk) provides multiple EC2 instances with load balancing.
* Amazon provides FREE SSL/TLS certificates for any domain behind an Elastic Load Balancer (i.e., Elastic Beanstalk).

Cons:
* No free compute instances after first year (Google doesn't provide free Flexible App Engines either).
* Elastic Beanstalk is more expensive than Google App Engine.
* CodeStar is designed for projects on CodeCommit only.
* Mirroring a GitHub repository to CodeCommit is not automated.
* You'll need to learn about VPCs, NATs, and subnets.

Sample Pricing:
* Lightsail (VM): $5.00/mo (1 core, 0.5GB RAM, 20 GB SSD)
* EC2 (t2.nano): $5.00/mo (1 instance, 1 core, 0.5GB RAM)
* EC2 (t1.micro): $15.00/mo (1 instance, 1 core, 1GB RAM)
* Elastic Beanstalk: $48.50/mo (2 EC2 t1.micro instances, 1 Elastic load balancer, 8GB SSD shared)

### EC2
> Resizable compute capacity in the cloud.
* 1 core, 0.5GB RAM
* Free for 12 months, $15/mo plus $0.10/GB SSD storage after.

### DynamoDB
> Fast and flexible NoSQL database with seamless scalability.
* 25GB of storage.

### Storage Gateway
> Hybrid cloud storage with seamless local integration and optimized data transfer.
* 100GB per month.

### Lambda
> Service that runs your code in response to events and automatically manages the compute resources.
* 1,000,000 requests per month.
* 400,000 GB/s compute time.

### Code Commit
> Highly scalable, managed source control service.
* Unlimited repositories.
* 50 GB-month of storage.
* 10,000 Git requests/month.
* Up to 5 active users per month.


## Microsoft Azure
Pros:
* $200 free credit to start.
* App Service supports containers so you don't have to use the default configurations.
* Cosmos DB (paid only) allows you to use SQL or MongoDB APIs, or even vanilla JavaScript.
* Free tier includes familiar databases like MySQL and PostgreSQL

Cons:
* Doesn't offer as many features as Amazon or Google in the free tier.
* Google and Amazon have better tutorials (personal opinion).

Sample Pricing:
* Virtual Machine: $14.88/mo (1 core, 0.75GB RAM, 20GB HDD, Ubuntu or Windows)
* Cloud Storage: $0.03/mo (1GB with 10,000 transactions)
* Cosmos DB: $25.30/mo (10GB SSD)

### App Service
* Up to 10 apps (60 CPU minutes per day per app).
* Shared cores, 1GB RAM, 1GB storage.

### Azure Database for MySQL or PostgreSQL
* 50GB storage.

### Functions
* 1,000,000 executions.
* 400,000 GB/s compute time.
