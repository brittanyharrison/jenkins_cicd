# CICD with Jenkins 

## CI/CD
CI/CD is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts attributed to CI/CD are continuous integration, continuous delivery, and continuous deployment.

## Jenkins 
Jenkins is a free and open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.

![IMG](img/CICD-1.jpg)

## Setting up a Job in Jenkins 
 
**Step 1: Create new item**
- On the left you should see `New item`, select that. 

**Step 2: Create job**
- Under `Enter an item anme` write the appropriate name for your job 


## SSH Connection Between Github and Jenkins 

**Step 1: Generate a new key**
- Generate a new ssh key in your localhost and name is YOURNAMEjenkins(eg brittanyjenkins). Steps to gerating a key can be found [here](https://github.com/brittanyharrison/engi_89_github_setup#step-2-generate-ssh-key). 

**Step 2: Copy Key into Github**
- Go into your repo and select `Settings`
- Select `Deploy Keys` and select `Add deploy key`
- Copy the public ssh key into `key` and title YOURNAMEjenkins 
- Now select `Add key`

**Step 3: Connect to Jenckins**
- Create a new Jenkins item and select `Freestyle Project`

Set up the following configurations:

- **Discard old builds**: 3
- **Github project**: Insert GitHub HTTPS repo link 
- **Restrict where this project can be run**: logical expression to specify which agent to execute builds of the project (e.g. sparta-ubuntu-node)
- **Git**:
    - **Repository URL**: Insert GitHub SSH repo link 
    - **Credential**: Add -> Jenkins -> Key -> Insert private ssh key 
- **Branches to build**: */main
- **Github hook trigger for GITScm polling**: check this option 

## Setting Up a Webhook
Setting up the webhook allows GitHub to trigger Jenkins to start a new build whenever a new commit is pushed.

In the GitHub repository that is to be linked to Jenkins, create a new Webhook (Settings-->Webhooks-->Add webhook)

Payload URL: Add the URL (usually specified with ip and port) with /github-webhook/ appended at the end
Content type: Select application/json
Any new pushes to the repository should now trigger a new build, shown in Build History where the Console Output can be read for each individual build