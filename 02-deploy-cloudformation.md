## Context

We have prepared [git repo](https://github.com/arief-hidayat/odoo-ecs) which contains [CDK](https://aws.amazon.com/cdk/) project.

## Prepare Repo

Clone repo

```
git clone https://github.com/arief-hidayat/odoo-ecs.git
cd odoo-ecs/
npm install
cdk bootstrap

```

Open file `odoo-ecs/lib/odoo-ecs-stack.ts`

![ecs stack](./static/004b-odoo-ecs-stack.jpg)

Edit email and VPC name. firstTime to `true`

```
    const emailAddress = 'mr.arief.hidayat@gmail.com';
    ...
    const firstTime = false;
    ...
    const vpc = ec2.Vpc.fromLookup(this, 'dev-vpc', {vpcName: 'AriefhInfraStack/dev-vpc'});
```

generate cloudformation template 

```
cdk synth
```

### Deploy
deploy

```
cdk deploy
```
see CloudFormation in progress

![cloudformation in progress](./static/004c-cloudformation-in-progress.jpg)

First time setup will take longer time for Database

![rds](./static/004d-rds-in-progress.jpg)

Wait until completed

![complete](./static/004e-cloudformation-output.jpg)


### Verify

Go to `Secrets Manager`

![to sm](./static/005a-to-secret-manager.jpg)

Click `odoo-dev-app-pwd`, scroll down a bit and click `Retrieve Secret Value`.

![odoo-dev-app-pwd](./static/005b-odoo-dev-app-pwd.jpg)

Open Odoo URL from CloudFormation output `OdooEcsStack.odooLoadBalancer` and login using email and password from the secret.
![odoo login](./static/005c-login-to-odoo.jpg)

Now we are logged into Odoo
![odoo logged in](./static/005d-logged-in.jpg)


