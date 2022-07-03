pipeline {
    agent any
    environment {
        GitBranch = "packer"
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
                dir("DeployPacker") {
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
        stage("Create AMi ") {
            steps {
                dir("DeployPacker") {
                    sh "packer build -var 'port=$PORT' portAMI.json"
                }
            }
        }
    }
}
