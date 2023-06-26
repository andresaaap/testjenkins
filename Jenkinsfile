

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello"'
            }
        }

        // Publish over ssh the file andres.txt with configName Host2

        stage('Deploy') {
            agent any
            steps {
                sshPublisher(
                continueOnError: false, 
                failOnError: true,
                publishers: [
                    sshPublisherDesc(
                    configName: "Host2",
                    transfers: [sshTransfer(sourceFiles: 'andres.txt')],
                    verbose: true
                    )
                ]
                )
            }
            }
    }
}