# MLOps with CI/CD on local Git repository

Train, deploy, and host your models on AWS.

## 1. Prerequisites

*Open your AWS account*



*Create a GitHub repository and user token (save locally as e.g. in a text file)*



*Clone the new GitHub repository to your local Git repository folder*



*Download the code, and unzip it to the local Git repository folder*



*Push to the main branch*



## 2. Create the MLOps pipeline

*Navigate to the CloudFormation service*



*Select Create stack*



*Select Upload template file and upload the YAML file from the infrastructure folder called `infra/pipeline.yml`*



*Specify the stack details. These include:*

- **Stack name:** mlpipeline
- **Email:** Kyriacos@smartworkz.nl (to receive SNS notification)
- **GitHub Token:** {previously generated and saved locally}
- **GitHub User:** smartworkz-kyriacos
- **GitHub Repository:** mlops-sagemaker-ci-cd
- **Branch:** master (main)



*Click Next in the Configure stack options page*



*Acknowledge that CloudFormation might create IAM resources with custom names and click Create stack*



*You will see the stack creation which should be complete within some minutes.*



## 3. Run the MLOps pipeline

*Navigate to the CodePipeline service*



*Select your created pipeline*



*The steps include:*

- **Source:** pulls code every time submit changes. Can be triggered manually by clicking on the Release change button.
- **Build_and_train:** executes the `source\training.py` script. This downloads the data uploads to an S3 bucket creates a training job and deploys the model
- **Test_Model:** executes the `source\test.py`  script that performs a basic test of the deployed model



## 4. Use GPU and Spot instances



## 5. Add the training job dependencies



## 6. Trigger training job from the local Git repository



## 7. Deploy with Lambda function

