# Packer Nodejs Read Me

## What is packer?

packer is used to create an image. These images can be used as testable environments.

## How to use the repo to create AMI for environments.

First you need to install packer. You can check you have it by running.
```
packer verify
```

after you need to get the packer.json working correctly.

You will need to add your pem keys to the packer.json file so the image is accessible for you.

**go into the packer.json and edit the following**
```
"ssh_keypair_name": "<YOUR KEY>",
"ssh_private_key_file": "<YOUR KEY>",
```
You will also need to edit the AWS Access and Secret keys.
- Please set the environment variable.
To do this run the command:

**go into the packer.json and edit the following**
```
cd ~
```
then -
```
sudo nano .zshrc
```

Go to the bottom of the file and edit as follows:

**go into the .zshrc and edit the following**
```
export AWS_ACCESS_KEY_ID=<YOUR ACCESS KEY>
export AWS_SECRET_ACCESS_KEY=<YOUR SECRET ACCESS KEY>
```
ensure your environment variable name is the same in both your .zshrc and your packer file.

**go into the packer.json and edit the following**
```
"aws_access_key": "{{env `AWS_ACCESS_KEY_ID`}}",
"aws_secret_key": "{{env `AWS_SECRET_ACCESS_KEY`}}"
```
you can name your AMI by editing your packer.json

**go into the packer.json and edit the following**
```
"ami_name": "<YOUR NAME HERE>-{{timestamp}}"
```

To check you have everything correct go into the terminal and run the command:
```
packer validate packer.json
```
This should return:
*Template validated successfully.*

Finally you need to build your AMI so you can have an environment to work on.To build an AMI go into the terminal and run the command:
```
packer build packer.json
```

## Pre-requisites.

- oh my zssh (command line)
- packer
