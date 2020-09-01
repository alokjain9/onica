# CloudFormation: How to run templates


## Cloning CodeCommit Repo

You can install Git following the instructions [here](https://www.atlassian.com/git/tutorials/install-git).
Use **git credentials** provided in the assignment email to clone the CodeCommit repository.

**Important for Mac Users:**
If running `git clone` command below results in *Unable to access: 403* error, follow this [link](https://stackoverflow.com/questions/34517534/running-git-clone-against-aws-codecommits-gets-me-a-403-error) to troubleshoot Keychain Access issue.

```shell 
git clone https://git-codecommit.us-west-2.amazonaws.com/v1/repos/onica-careers-ce-candidates

cd onica-careers-ce-candidates/cfn
```

## Pre-requisite to run CloudFormation

Create Access Key by logging into AWS console with provided credentials.

Configure AWS CLI to launch CloudFormation scripts from terminal (see instructions [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html#cli-quick-configuration)).

## Deployment

### Order of execution

The template `ce-express-cf_vpc_bad.yaml` needs to be executed first and completed before executing any of the `ce-express-cf_WebServ` templates.

### Console Execution

* Login and navigate to AWS management console.
* Go to CloudFormation service.
* Switch to **us-west-2** region. 
* Launch a new stack via `Create Stack` button.

### CLI Execution

To run `ce-express-cf_vpc_bad.yaml` execute the following from inside the corresponding cfn folder.

```shell
aws cloudformation deploy \
    --stack-name ce-example-vpc \
    --region us-west-2 \
    --template-file ce-express-cf_vpc_bad.yaml
```

To run any of the `ce-express-cf_WebServ*` execute the following from inside the cfn folder.

For Linux:

```shell
aws cloudformation deploy \
    --stack-name ce-example-app-lnx \
    --region us-west-2 \
    --template-file ce-express-cf_WebServ_LNX_bad.yaml \
    --capabilities CAPABILITY_IAM 
``` 
or for Windows:

```shell
aws cloudformation deploy \
    --stack-name ce-example-app-win \
    --region us-west-2 \
    --template-file ce-express-cf_WebServ_WIN_bad.yaml \
    --capabilities CAPABILITY_IAM 
``` 

## Clean Up
When you are done ***(everything tested)***, log into management console and delete CFN stacks in the following order:

1. ce-example-app-lnx/win
2. ce-example-vpc

## Submitting the Test

Upon completing the assignment, do the following to submit it:
1. Clone the latest version of CodeCommit repository that has all your changes
2. ZIP the cloned repository including all relevant files.
3. Upload the code to the link provided with the assignment email. (https://app2.greenhouse.io/tests/<your_unique_number>
4. (optional) Notify the recruiting team the assignment has been submitted.

---