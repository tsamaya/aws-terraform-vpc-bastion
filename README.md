# aws-terraform-vpc-bastion

## Getting Started

- Install the AWS CLI from https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html on your environment.

- Install the terraform from https://www.terraform.io/downloads.html on your dev environment.

- Create a key-pair in the AWS region used to provision the infrastructure.

```bash
export STAGE=dev
export AWS_REGION=eu-west-1
export AWS_KEY_PAIR_NAME="bastion-${STAGE}-${AWS_REGION}"

aws ec2 create-key-pair \
       --key-name $AWS_KEY_PAIR_NAME \
       --query 'KeyMaterial' \
       --output text > "${AWS_KEY_PAIR_NAME}.pem"
```

Do not forget to backup this keypair file somewhere safe

- Clone this repository and edit the `variables.tf` file with the below mandatory parameters:

  1. key_name : <key_name >
  2. region : <region>
  3. product : <product>
  4. availability_zones : < 3 availability_zones>

## Reources

Gets the AMI-ID of the Ubuntu server for your region:

```bash
aws ssm get-parameters --region $AWS_REGION --names \
     /aws/service/canonical/ubuntu/server/20.04/stable/current/amd64/hvm/ebs-gp2/ami-id
```

## Cleanup

```bash
aws ec2 delete-key-pair \
       --key-name $AWS_KEY_PAIR_NAME
```
