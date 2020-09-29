# AWS CLI Scripts

These files can be used to create an EC2 instance where you will setup a Confluent Platform.

## Prerequisite
You have a local environment where you can run AWS CLI as well as the AWS environment where you will create your Confluent Platform.

## Preparation

Copy the following files and save without `.template` suffix.

- personal.config.template
- cli_input.json.template

Please replace `<YOUR__...>` in `cli_input.json` with the values for your AWS environment.

```
    "ImageId": "<YOUR_AMI_ID_IN_YOUR_REGION>",
    "KeyName": "<YOUR_KEY_NAME_WO_FILE_EXTENSION>",
    "SecurityGroupIds": [
         "<YOUR_SECURITY_GROUP_ID>"
    ],
...
    "SubnetId": "<YOUR_SUBNET_ID>",
```

Please replace `<YOUR_...>` in `personal.config` with the values for your AWS environment.

```
KEY_NAME=~/<YOUR_KEY_NAME_WO_FILE_EXTENSION>
REGION=<YOUR_REGION>
...
```

Please also replace `<..._AS_YOU_LIKE>` in `personal.config` with any appropriate values.

```
INSTANCE_NAME=<INSTANCE_NAME_PREFIX_AS_YOU_LIKE>
TAG_PROJECT=<PROJECT_AS_YOU_LIKE>
TAG_OWNER=<OWNER_AS_YOU_LIKE>
```

## Create an Instance

Execute `create_instance.sh` on your local environment.
```
$ create_instance.sh
```

Upon successful completion of the above script, you would find a new instance is created on AWS.


## Setup Passwordless Login
When you execute the above script, you would find `passwordless_<INSTANCE_NAME_AS_YOU_LIKE>_<DATA_TIME>.sh` is generated locally.
You can use this script to enable passwordless (no need to use PEM file) login.
When you use this script, you must run the script after you confirm your instance is up and running on AWS.


