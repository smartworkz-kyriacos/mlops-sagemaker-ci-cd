# MLOps with CI/CD on local Git repository

Train, deploy, and host your models on AWS.

## 1. Prerequisites

- *Open and log in to your [AWS account](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fus-east-1.console.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26nc2%3Dh_ct%26region%3Dus-east-1%26skipRegion%3Dtrue%26src%3Dheader-signin%26state%3DhashArgsFromTB_us-east-1_69d8e4b4ab0e37a6&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=uRVQqhamdm60rHPKKXydxDu4E3wcQICknuXn1V8seVo&code_challenge_method=SHA-256)*

- *Open and log in to your [GitHub account](https://github.com/)*

- If not already done, *Install [Visual Studio Code](https://code.visualstudio.com/download) (VSC)*

- If not already done, *Install [Git Bash](https://git-scm.com/downloads)*

- *(Optional) Configure Git Bash as the default terminal for VSC*

  	1. Click View, Terminal

  2. After the Terminal appears, press the F1 key

  3. Type the following, Terminal: Select Default Profile

  4. Select from the dropdown, Git Bash 

- *Download the [code](), and unzip it in the local Git repository folder path*. Your GitHub repository will now look similar to the one below

  ​		![](images/github.png)

- *`cmd` File Explorer in the path field*

1. Using File Explorer navigate to the local Git Repository

![](images/File explorer local Git Repository.png)

2. In the path field type cmd and press the Enter key

![](images/cmd.png)

- A cmd window opens in the repository path.

![](images/Win_Cmd-Prompt.png)

- *Type `code .` in the cmd window prompt with the path*

![](images/code.png)

- VSC opens automatically.

![](images/vsc.png)

- *Open* your GitHub account Repositories page

![](images/Full-Screen.png)

*Make sure the  Git Bash terminal is in VSC (arrange it side-by-side with the  GitHub page). *

![](images/Git-Bash-VSC.png)

Run the following commands:

```shell
#Configure global settings

git config --global user.name "Kyriacos Antoniades- Smartworkz"`		
git config --global user.email "Kyriacos@smartworkz.nl"`
git config --global push.default matching`
git config --global alias.co checkout`
git config --global credential.helper cache

#Check

git config --global user.name`
git config --global user.email`

#Initialize

git init`
git status`
git add .`
git commit -m "MLOPs code remote upload from the local repository"
```

```shell
#Push to the main branch*

git push
```

- *Create a GitHub  Personal Access Token (PAT)*

1. In the upper-right corner of any page, click your profile photo, then click **Settings**.

   ![Settings icon in the user bar](https://docs.github.com/assets/cb-34573/images/help/settings/userbar-account-settings.png)

2. In the left sidebar, click **Developer settings**.![Developer settings](https://docs.github.com/assets/cb-6064/images/help/settings/developer-settings.png)

3. In the left sidebar, click **Personal access tokens**.![Personal access tokens](https://docs.github.com/assets/cb-7169/images/help/settings/personal_access_tokens_tab.png)

4. Click **Generate new token**.![Generate new token button](https://docs.github.com/assets/cb-6922/images/help/settings/generate_new_token.png)

5. Give your token a descriptive name.![Token description field](https://docs.github.com/assets/cb-3880/images/help/settings/token_description.png)

6. To give your token an expiration, select the **Expiration** drop-down menu, then click a default or use the calendar picker.![Token expiration field](https://docs.github.com/assets/cb-39847/images/help/settings/token_expiration.png)

7. Select the scopes or permissions, you'd like to grant this token. To use your token to access repositories from the command line, select **repo**.

   ![Selecting token scopes](https://docs.github.com/assets/cb-43299/images/help/settings/token_scopes.gif)

8. Click **Generate token**.![Generate token button](https://docs.github.com/assets/cb-10912/images/help/settings/generate_token.png)

   ![Newly created token](https://docs.github.com/assets/cb-31676/images/help/settings/personal_access_tokens_ghe.png)

   **Warning:** Treat your tokens like passwords and keep them secret. When working with the API, use tokens as environment variables instead of hardcoding them into your programs.

Save locally e.g. in a text file. Will be used shortly to specify in the stack details later. Once you have a token, you can enter it instead of your password when performing Git operations over HTTPS. For example, on the command line you would enter the following:

```shell
$ git clone https://hostname/USERNAME/REPO.git
Username: YOUR_USERNAME
Password: YOUR_TOKEN
```

## 2. Create the MLOps pipeline

- *Navigate to the [CloudFormation service](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Feu-west-1.console.aws.amazon.com%2Fcloudformation%2Fhome%3Fregion%3Deu-west-1%26state%3DhashArgs%2523%252F%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fcloudformation&forceMobileApp=0&code_challenge=2wvOgJKH4gI44qKCepanh-y6BA4SLHzP7S2hxNBhcJo&code_challenge_method=SHA-256)*

- *Select Create stack*

![](images/01_cloudformation.png)

- *Select Upload template file and upload the YAML file from the infrastructure folder called `infra/pipeline.yml`*

![](images/02_cloudformation_create_stack.png)

- *Specify the stack details. These include:*
  - **Stack name:** mlpipeline
  - **Email:** Kyriacos@smartworkz.nl (to receive SNS notification)
  - **GitHub Token:** {previously generated and saved locally}
  - **GitHub User:** smartworkz-kyriacos
  - **GitHub Repository:** mlops-sagemaker-ci-cd
  - **Branch:** master (main)

![](images/mlops_03_cloudformation_specify_stack.png)

- *Click Next in the Configure stack options page*

![](images/04_cloudformation_configure_stack.png)

- *Acknowledge that CloudFormation might create IAM resources with custom names and click Create stack*

- *You will see the stack creation which should be complete within some minutes.*

![](images/06_cloudformation_create_in_progress.png)

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

