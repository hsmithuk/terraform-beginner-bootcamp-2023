# Terraform Beginner Bootcamp 2023

## Semantic Versioning

This project is using semantic versioning for its tagging.
[semver.org](https://semver.org)

This is using a general version number **MAJOR.MINOR.PATCH**, e.g.  `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

Shebang at [wiki shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))
https://www.gitpod.io/docs/configure/workspaces/tasks

### Install the Terraform CLI
The CLI instuctions have changed.   Had to use commands found at [Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
So the original gitpod.yml bash would not run. 

We removed lines 3-11:
`    init: |
      sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
      curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
      sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
      sudo apt-get update && sudo apt-get install terraform
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
    `
Replaced with:
`    before: |
     source ./bin/install_terraform_cli
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    before: |
`
Much less text !
 So replaced it with values found now under. `/workspace/terraform-beginner-bootcamp-2023/bin/install_terraform_cli`
Ran these to validate, then replaced prior values with the new one.  As validation tests ( running in CLI) worked well.

[Checking linux version] cat /etc/os-release

[Changing file version permission value]

- **Using Chmod**
Imagine you are attemoting to run command:  `./bin/install-terraform_cli`
It returns error. of  ;'Permission Denied`.

Viewing. `gitpod /workspace/terraform-beginner-bootcamp-2023 (3-refactor-terraform-cli)`

`ls -la ./bin` 

'total 4
drwxr-xr-x 2 gitpod gitpod  35 Oct 28 20:52 .
drwxr-xr-x 4 gitpod gitpod 113 Oct 28 20:52 ..
-rw-r--r-- 1 gitpod gitpod 570 Oct 28 21:40 install-terraform_cli
'

We want the last file not to be:   File says. @ -rw-r--r--    
 But to say : -rwx-r--r--

 Using chmod then following: 
 chmod u+x ./bin/install_terraform_cli


`chmod u+x ./bin/install-terraform_cli`
`ls -la ./bin
total 4
drwxr-xr-x 2 gitpod gitpod  35 Oct 28 20:52 .
drwxr-xr-x 4 gitpod gitpod 113 Oct 28 20:52 ..
-rwxr--r-- 1 gitpod gitpod 570 Oct 28 21:40 install-terraform_cli`

So now the file is -rwxr

To make all the files in a folder read/write.  @chomd 777
