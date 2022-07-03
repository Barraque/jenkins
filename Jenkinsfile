pipeline {
    agent any
    environment {
        GitBranch = "port"
    }
    
    stages {
        stage("Clen Jenkins Workspace before start") {
            steps {
                cleanWs()
            }
        }
        stage("checkout git") {
            steps {
                sh "pwd"
                dir("DeployApp") {
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
        stage("Deploy APP") {
            steps {
                dir("DeployApp") {
                    sh "pwd"
                    sh "ls"
                    
                    sh "terraform init -backend-config='bucket=bucketdemorts' -backend-config='key=$APP_NAME/$ENV/terraform.tfstate' -backend-config='region=eu-west-1'"
                    sh "terraform apply -auto-approve"
                }
            }
        }
        
        
    }
}
