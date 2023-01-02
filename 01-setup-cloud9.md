
## Setup

In this section, we will setup Cloud9 environment.

### Prepare IAM Roles for Cloud9 to Access Services

Go to `IAM` console. Select `Role` on the left menu. Then click `Create Role` button

![go to iam role](./static/003a-to-iam-role.jpg)

Select `AWS Service` and for `EC2` use case.

![go to iam role](./static/003b-create-for-ec2.jpg)

Search permission policy `AdministratorAccess` and tick the checkbox.

![admin](./static/003c-admin.jpg)


### Create Cloud9

Go to `Cloud9` console

![go to cloud9](./static/002a-to-cloud9.jpg)

Click `Create Environment`

![create environment](./static/002b-create-env.jpg)

Choose EC2 instance type. `t3.small` is good enough

![choose instance](./static/002c-t3-small.jpg)

Put it in our newly created VPC

![set VPC](./static/002d-use-our-vpc.jpg)

Use one of our private subnets

![set VPC](./static/002e-use-private-subnet.jpg)

Click `Create` button

![create env](./static/002f-create.jpg)

Once created, click `open`

![open env](./static/002g-created.jpg)

It will run the instance

![instance running](./static/002h-open-cloud9.jpg)

Back to the `cloud9` console, click name to see detail page

![cloud9 page](./static/002g-created.jpg)

Click `Manage EC2 Instance`

![manage ec2 instance](./static/002i-open-cloud9-detail.jpg)

New tab to `EC2` will be opened, click the checkbox

![select ec2](./static/002j-in-ec2-console.jpg)

Select from dropdown menu `Action` -> `Security` -> `Modify IAM Role`

![modify iam role](./static/002k-modify-iam-role.jpg)

Select IAM role we just created in previous step from dropdown menu.

![select iam role](./static/002l-update-iam-role.jpg)

Click `Update IAM Role`

![update iam role](./static/002m-update-iam-role.jpg)

### Prepare Credentials

disabling AWS managed temporary credentials for Cloud9

![no aws managed creds](./static/004a-no-managed-temporary-creds.jpg)

To ensure temporary credentials aren’t already in place we will remove any existing credentials file.

```
rm -vf ${HOME}/.aws/credentials
```

We should configure our aws cli with our current region as default.

```
echo "export AWS_DEFAULT_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)" >> ~/.bashrc
echo "export AWS_REGION=\$AWS_DEFAULT_REGION" >> ~/.bashrc
echo "export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)" >> ~/.bashrc
source ~/.bashrc
```