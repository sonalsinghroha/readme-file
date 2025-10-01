#  POC: Terraform Wrapper using Jenkins Shared Library

## Author Information

| Created by | Created on | Version | Last Updated On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------- | ---------- | ------- | --------------- | ------------ | ----------- | ----------- | ----------- |
| Sonal      | 17-09-2025 | V 1.0   | 17-09-2025      | Neelesh      |             |             |             |


## Table of Contents

- [Introduction](#Introduction)
- [Project Directory Structure](#project-directory-structure)
- [Terraform Code (infra/terraform)](#terraform-code-infraterraform)
- [Shared Library Wrapper (Wrapper.groovy)](#shared-library-wrapper-wrappergroovy)
- [Jenkinsfile](#jenkinsfile)
- [How to Run the POC](#how-to-run-the-poc)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---


##  Introduction

This Proof of Concept (POC) demonstrates the use of a Jenkins Shared Library to wrap Terraform CLI commands (`init`, `validate`, `plan`, `apply`, `destroy`). It includes:

- A minimal Terraform configuration
- A shared Groovy class wrapping Terraform commands
- A Jenkinsfile that calls the wrapper
- Directory layout
- Expected Jenkins pipeline behavior

---

## Project Directory Structure
### Repo 1: `terraform-wrapper-code`
This is your project repo that runs the Jenkins pipeline.

```pgsql
terraform-wrapper-code/
├── Jenkinsfile
├── terraform/
│   ├── main.tf
│   ├── terraform.tfvars
│   └── variable.tf
└── README.md
```
### Repo 2: `shared-libraryy`
This is your shared library repo used by Jenkins.

```pgsql
shared-libraryy/
├── vars/
    └──terraformPipeline.groovy
├── src/
│   └── org/
│       └── cloudninja/
│           └── Wrapper.groovy
└── README.md
```
---

##  Terraform Code (infra/terraform)

### `main.tf`

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "demo_bucket" {
  bucket = var.bucket_name
}

output "bucket_name" {
  value = aws_s3_bucket.demo_bucket.id
}
```
### `variable.tf`
```hcl
variable "region" {
  default = "ap-south-1"
}

variable "bucket_name" {
  description = "S3 bucket name"
}
```
### `terraform.tfvars`
```hcl
bucket_name = "demo-wrapper-s3-bucket"
```
---

## Wrapper.groovy
```groovy
package org.cloudninja  

class Wrapper implements Serializable {
    def steps

    Wrapper(steps) {
        this.steps = steps
    }

    def init(String dir = 'terraform') {
        steps.echo " Running: terraform init in '${dir}'"
        steps.dir(dir) {
            steps.sh 'terraform init'
        }
    }

    def validate(String dir = 'terraform') {
        steps.echo " Running: terraform validate in '${dir}'"
        steps.dir(dir) {
            steps.sh 'terraform validate'
        }
    }

    def plan(String dir = 'terraform', String varFile = 'terraform.tfvars') {
        steps.echo " Running: terraform plan in '${dir}' with '${varFile}'"
        steps.dir(dir) {
            steps.sh "terraform plan -var-file=${varFile}"
        }
    }

    def apply(String dir = 'terraform', String varFile = 'terraform.tfvars') {
        steps.echo " Running: terraform apply in '${dir}' with '${varFile}'"
        steps.dir(dir) {
            steps.sh "terraform apply -auto-approve -var-file=${varFile}"
        }
    }

    def destroy(String dir = 'terraform', String varFile = 'terraform.tfvars') {
        steps.echo " Running: terraform destroy in '${dir}' with '${varFile}'"
        steps.dir(dir) {
            steps.sh "terraform destroy -auto-approve -var-file=${varFile}"
        }
    }
}
```

## terraformPipeline.groovy
```groovy
def call(Map config = [:]) {
    def terraformDir = config.get('terraformDir', 'terraform')
    def tfVarsFile = config.get('tfVarsFile', 'terraform.tfvars')
    def destroyParam = config.get('destroyParam', 'DESTROY_INFRA')
    def credentialsId = config.get('credentialsId', 'aws-keys')

    def tf = new org.cloudninja.Wrapper(this)

    pipeline {
        agent any

        parameters {
            booleanParam(name: destroyParam, defaultValue: false, description: 'Destroy infrastructure?')
        }

        environment {
            TF_IN_AUTOMATION = 'true'
        }

        stages {
            stage('Debug Branch Info') {
                steps {
                    echo "Branch Info - BRANCH_NAME: ${env.BRANCH_NAME}, GIT_BRANCH: ${env.GIT_BRANCH}"
                }
            }

            stage('Terraform Init & Validate') {
                steps {
                    withCredentials([usernamePassword(credentialsId: credentialsId, usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        script {
                            tf.init(terraformDir)
                            tf.validate(terraformDir)
                        }
                    }
                }
            }

            stage('Terraform Plan') {
                steps {
                    script {
                        tf.plan(terraformDir, tfVarsFile)
                    }
                }
            }

            stage('Terraform Apply') {
                when {
                    allOf {
                        anyOf {
                            branch 'main'
                            expression { env.GIT_BRANCH == 'main' || env.GIT_BRANCH == 'origin/main' }
                        }
                        not { expression { params[destroyParam] } }
                    }
                }
                steps {
                    script {
                        tf.apply(terraformDir, tfVarsFile)
                    }
                }
            }

            stage('Terraform Destroy') {
                when {
                    expression { return params[destroyParam] }
                }
                steps {
                    script {
                        input message: "Are you sure you want to destroy the infrastructure?"
                        tf.destroy(terraformDir, tfVarsFile)
                    }
                }
            }
        }

        post {
            success {
                echo " Terraform pipeline completed successfully!"
            }
            failure {
                echo " Terraform pipeline failed."
            }
            always {
                echo " Terraform pipeline execution finished."
            }
        }
    }
}
```
## Jenkinsfile
```groovy
@Library('shared-libraryy') _

terraformPipeline(
    terraformDir: 'terraform',
    tfVarsFile: 'terraform.tfvars',
    destroyParam: 'DESTROY_INFRA',
    credentialsId: 'aws-keys'
)
```

---

## How to Run the POC
- Register the shared library in Jenkins → Manage Jenkins → Configure System:

Library Name: terraform-wrapper-lib

Source Code: Point to your Git repo (or local folder if testing locally)

- Create a Jenkins pipeline job and point it to the Jenkinsfile.

- Trigger the job with default (DESTROY = false) to run init → validate → plan → apply.

- Trigger again with DESTROY = true to test destroy.

---

## Conclusion
This POC demonstrates how to use wrapper code with shared library in Terraform.

---


## Contact Information

| Name  | Email                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Sonal | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## References

| Title                                 | Link                                                                                    |
| ------------------------------------- | --------------------------------------------------------------------------------------- |
| Terraform CLI                         | [Link](https://developer.hashicorp.com/terraform/cli)                                   |
| Jenkins Shared Libraries              | [Link](https://www.jenkins.io/doc/book/pipeline/shared-libraries/)                      |
| Automating Terraform with Jenkins     | [Link](https://learn.hashicorp.com/tutorials/terraform/automate-terraform-with-jenkins) |
| Best Practices for Terraform in CI/CD | [Link](https://www.terraform.io/language/expressions/ci-cd)                             |
