pipeline {
    agent any
    environment {
        GitBranch = "main"
    }
    
    stages {
        stage("Clen Jenkins Workspace before start") {
            steps {
                cleanWs()
            }
        }
        stage("check Vars"){
            steps {
                sh "echo $APP_NAME"
                sh "echo $ENV"
            }
        }
        stage("checkout git") {
            steps {
                sh "pwd"
                dir("DeployInfra") {
                    sh "pwd"
                    git(
                        url: 'git@github.com:Barraque/tpaws.git',
                        credentialsId: 'github',
                        branch: "${GitBranch}"
                        )
                    sh "ls"
                }
            }
        }
        stage("Deploy Infra") {
            steps {
                dir("DeployInfra") {
                    sh "pwd"
                    sh "ls"
                    
                    sh "terraform init -backend-config='bucket=bucketdemorts' -backend-config='key=$APP_NAME/$ENV/terraform.tfstate' -backend-config='region=eu-west-1'"
                    sh "terraform apply -auto-approve"
                }
            }
        }
        
        
    }
}
