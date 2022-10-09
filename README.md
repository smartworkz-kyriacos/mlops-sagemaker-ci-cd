# MLOps with CI/CD on local Git repository

Train, deploy, and host your models on AWS.

## 1. Prerequisites

*Open your [AWS account]()*

*Open your [GitHub account]()*

*Install [Visual Studio Code]() (VSC)*

*Install [Git Bash]()*

*Configure Git Bash as the default terminal for VSC*

*Download the [code](), and unzip it in the local Git repository folder path*

*`cmd` File Explorer in the path field*

*`code .` in the cmd window prompt with the path*

*Open* your GitHub account Repositories page

*Open Git Bash terminal in VSC*

- #Configure global settings

​		`git config — global user.name "Kyriacos Antoniades- Smartworkz"`		

​		`		git config — global user.email "Kyriacos@smartworkz.nl"`

​		`		git config — global push.default matching`

​		`git config — global alias.co checkout`

- #Check

​		`git config — global user.name`

​		`git config — global user.email`

​		`git init`

​		`git status`

​		`git add .`

​		`git commit -m "MLOPs code remote upload from the local repository"`

- *#Push to the main branch*

​		`git push`

*Create a GitHub  user token (save locally as e.g. in a text file)*



## 2. Create the MLOps pipeline

- *Navigate to the CloudFormation service*



- *Select Create stack*



- *Select Upload template file and upload the YAML file from the infrastructure folder called `infra/pipeline.yml`*



- *Specify the stack details. These include:*
  - **Stack name:** mlpipeline
  - **Email:** Kyriacos@smartworkz.nl (to receive SNS notification)
  - **GitHub Token:** {previously generated and saved locally}
  - **GitHub User:** smartworkz-kyriacos
  - **GitHub Repository:** mlops-sagemaker-ci-cd
  - **Branch:** master (main)



- *Click Next in the Configure stack options page*



- *Acknowledge that CloudFormation might create IAM resources with custom names and click Create stack*



- *You will see the stack creation which should be complete within some minutes.*



## 3. Run the MLOps pipeline

- *Navigate to the CodePipeline service*



- *Select your created pipeline*



- The steps include: 
  - **Source:** pulls code every time submit changes. Can be triggered manually by clicking on the **Release change** button.
  - **Build_and_train:** executes the `source\training.py` script. This downloads the data uploads to an S3 bucket creates a training job and deploys the model
  - **Test_Model:** executes the `source\test.py`  script that performs a basic test of the deployed model



## 4. Use GPU and Spot instances

- *Modify `instance_type = "ml.p3.2xlarge"` in the `source\training.py` script*

- *In the `source\training.py` script uncomment these lines:*
  - ​	`	use_spot_instances = True		# Use a spot instance`
  - ​	`max_run = 300 					# Max training time`
  - ​	`	max_wait = 600 				# Max training time + spot waiting time`

- *Commit and push changes to your GitHub repository*

- *Navigate to SageMaker Training jobs, check to see Manage Spot Training Savings*



## 5. Add the training job dependencies

- *In the `source\training.py` script uncomment the following line `source_dir = "code`*

- *In the `source\training.py` script update entry_point to `entry_point="mnist.py"`*

## 6. Trigger training job from the local Git repository

- *Create AWS Access keys*

- *Install AWS CLI*

- *Set up your AWS CLI*

- *Create a virtual environment inside your project*

- *Install required dependencies*

- *Navigate to CloudFormation service stacks*

- *Select the stack created earlier and go to the output section*

- *Copy the ExampleLocalCommand*

- *In the command line replace MODEL-NAME and VERSION and execute* 

- *Navigate to SageMaker Training jobs, check to see Manage Spot Training Savings*

## 7. Deploy with Lambda function

- *Install Chalice*

- *Navigate to your SageMaker Endpoint in the AWS console and copy the name of the endpoint*

- *In the lambda\\.chalice\config.json update the value of the ENDPOINT_NAME environment variable with the name of your SageMaker endpoint*

- *Deploy the Lambda function*

- *Trigger your Lambda*

