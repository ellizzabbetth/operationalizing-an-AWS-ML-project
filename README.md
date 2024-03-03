
## Writeup

Computer Vision project: recognize types of dogs from images of dogs



Goal: Operationalize the project so it's ready to be deployed live in a real world application

Maxmize project speed and minimize cost
Setup a Lambda function
Resolve a security issue and check for security issues
distributed training
concurrency and autoscaling



The major steps of the project include

Deploy appropriate instances that allow you to maximize your projects’ speed and minimize costs.
Set up a Lambda function so the project can provide outputs to users.
Resolve a security issue related to your Lambda function, and check for other security issues.
Set up your model training so it can train on multiple instances simultaneously.
Set up concurrency and autoscaling for your project so it can manage high throughput with low latency.




## Step 1 : Training and deployment on Sagemaker

create and open a Sagemaker instance. For this project, X instance was chosen because it is a powerful GPU which had previously been granted access by AWS.

![](screenshots/sagemaker_instance_setup.png)


![](screenshots/notebook_setup.png)

![](screenshots/notebook_kernel.png)

![](screenshots/hyperparameter-tuning-jobs.png)


## Step 2: EC2 Training


open the TrainedModels directory on your EC2 instance and take a screenshot of the model that has been saved in it, to provide evidence that you completed this step
![](screenshots/ec2_setup.png)


https://knowledge.udacity.com/questions/924507

GPU based instance types such as p3 are the ideal ones, but have limits on the student accounts. It will work on t3.medium but the training will be very slow.

"Decide the type of instance you want, create it in your workspace, and write a justification of why you chose the instance type you did."

A:  t3.medium, Deep Learning AMI Neuron (Ubuntu 22.04) 

```
wget https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip
unzip dogImages.zip
```

```
mkdir TrainedModels
```

```
vim solution.py
```

```
:set paste
```


![](screenshots/ec2_connection.png)


![](screenshots/ec2_model_saved.png)


## Step 3: Lambda function setup


Write at least 1 paragraph describing how this function is written and how it works.

Configured a Lambda function to invoke the deployed endpoint. The lambda function has the 
appropriate security policy to allow the lambda function to access all of the Sagemaker endpoints.

![](screenshots/lambda_function.png)


Q: you should notice how it invokes the endpoint (with the invoke_endpoint() method) and how it sets up the return statement. Write at least 1 paragraph describing how this function is written and how it works.

A: 

## Step 4: Security and testing

![](screenshots/iam_security.png)

## Step 5: Concurrency and auto-scaling

The purpose of concurrency on the lambda function is to accomodate high traffic because it will enable 
the function to respond to more than one invocation at once.

https://stackoverflow.com/questions/70279196/why-is-configure-autoscaling-greyed-out-on-sagemaker