*Notes for Interstella 8888 - Docker with AWS*

As you install images, it will become read only after it has been established. highest layer is read/write. i.e. OS read, nginx read, etc.

API Key: Q316lUkTzv5aUWO4F1UnT6OYCHRrkPrOav79hW4P

*Notes for Serverless Backend*

1. Create a static web hosting for index.html
2. Create SNS Topic for Contact Us
3. Add subscriber for SNS Topic
4. Create Lambda Function
5. Create API Gateway with Lambda Function
6. Submit

CICD 

Source
	Version Control
	Branching (Gitful - Feature Branching)
	Code Review

Build
	Compilation
	Unit Tests
	Static Analysis
	Packaging

Test
	Integration Tests
	Load Tests
	Security Tests
	Acceptance Tests

Production
	Deployment
	Monitoring
	Measuring
	Validation

CI => Source => Build
CD => Source => Production
(Continuous Delivery) / (Continuous Deployment)

Final Commit = Sum of all the layer of commits belkow it

NodeJS - How to avoid running npm install everytime (Dockerfile)

	from nodejs
	add package.json
	run npm install
	add /src
	cmd node app.js

What you want for versioning:
	microservice:1.0.0
	microservice:1.1.0
	microservice:1.1.1
	microservice:1.2.0


Have a Public Subnet for public facing services like (Orders, API Gateway), then Private Subnet with Passwords and Credit Cards. Load Balancer will connect to the public services... public services can connect to another load balancer that connects to the private services


1. Test app in local
2. Push/export code into CI machine
3. UAT - QA
4. Productoin

Deployment - In Place - Doubling
	Desired Count = 2
	Min Health Percent = 100%
	Max Percent = 200%

Deployment - In Place - Rolling
	Desired Count = 2
	Min Health Percent = 50%
	Max Percent = 100%

Deployment - Canary (Bird miners)
	Add a single new canary task to the cluster to see how it behaves.
	If it's good, then roll it out more

Deployment - Blue/Green - DNS Swap
	Two services are defined each with their own ALB
	Deployment is completed by swapping R53 alias record btwn two ALB
	An identical ALB and a service with a task def using new rev is deployed
	If things go wrong, can immediately swap CNAME/DNS back to original

Weighted Record Set
	Multiple values for DNS to resolve to, set wait times in case 
	ecs-canary-blue-green-deployment (github)

Best Practices
	- Use ELB health checks to prevent botched deploys
	- For higher confidence, integrate automated testing against a new environment or monitoring of a canary before cutover
	- Ensure your app can function against the same backend schema for adjacent releases

Deployment Pipeline
	Automated manifestation of the process for getting your software from version control and into the hands of your customer

Developers -> Github - > Jenkins -> DockerHub/Cloudformation -> ECS

Cloudformation = Infrastructure By Code

ecs-refarch-continuous-deployment (github)
awslabs
@nathankpeck


*Notes for Interstella 8888 - Monolith to Microservices*

Strangler Application Pattern


*Getting Started with Serverless Computing w/ Lambda*

Serverless means...
	
	No servers to provision or manage (Not Baremetal)
	Scales with usage
	Never pay for idle
	Availability and fault tolerance built in

Serverless applications
	
	Event Source => Function => Services

Common serverless use cases
	
	Web Apps (Static websites, Complex Web Apps, Packages for Flash/Exp)
	Backends (App & Service, Mobile, IoT)
	Data Processing (Real time, MapReduce, Batch)
	Chatbots
	Amazon Alexa (Powering voice enabled apps, Alexa skills kit)
	IT Automation (Policy engines, extending AWS Services, Infra Management)

Event-driven Compute => Functions as a Service => Serverless FaaS

Lambda Exec Model
	
	Synchronous (Push) 
		API Gateway -> /order -> Lambda Func
	
	Asynch (Event)
		SNS / S3 -> Reqs -> Lambda Func
	
	Stream-Based
		DynamoDB / Kinesis -> Changes -> AWS Lambda Service->Lambda Func
		(Database triggers)

Lambda Permission Model
	
	Exec Policies:
		Define what AWS resources
		Lambda func A can read from DynamoDB table users
	
	Func Policies
		Resource policies
		Actions on bucket X can invoke Lambda func Z

API Gateway
	
	Create a unified API frontend for multiple micro-services
	
	DDOS protection and thottling for your backend
	
	Authenticate and Auth requests to a backend
	
	Throttle, Meter, and Monetize API usage by third party developers

AWS Step Functions
	
	"Serverless" workflow management with zero admin
	
	- Make it easy to coordinate the compoonents of distributed applications and 
	microservices using visual workflows
	
	- Auto triggers and tracks each step, and retries when there are errors, so your application executes in order and as exptecd
	
	- Logs the state of each step so when things do go wrong, ou can diagnose and debug quickly

Amazon Lex
	
	Service for building conversational infterfaces into any application using voice and text
	
	Automatic speec recognition for converting speech to text
	
	Natural language understanding to recognize the intent of the messages
	
	Fully managed service

Lambda + Kinesis
	
	Realtime data processing:
	1. Realtime event data sent to Kinesis allows multiple Lambda funcs to process same events
	2. Func 1 processes and agg data from incoming events and store esult data
	3. Func 1 sends data to Cloudwatch for simple monitoring of metrics
	4. Func 2 does data manip of incoming events and stores results in S3

















