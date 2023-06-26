

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello"'
            }
        }

        stage('Publish Over SSH') {
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(configName: 'SSH_Config', transfers: [
                        sshTransfer(execCommand: "mkdir -p /home/ec2-user/newfiles", execTimeout: 120000),
                        sshTransfer(remoteDirectory: "/home/ec2-user/newfiles", sourceFiles: "andres.txt")
                    ])
                ])
            }
        }
    }
}