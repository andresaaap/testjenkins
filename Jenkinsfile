

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello"'
            }
        }

        // Publish over ssh the file andres.txt with configName Host2

       stage('SSH transfer') {
            steps([$class: 'BapSshPromotionPublisherPlugin']) {
                sshPublisher(
                    continueOnError: false, failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "Host2",
                            verbose: true,
                            transfers: [
                                sshTransfer(sourceFiles: "**.txt",)
                            ]
                        )
                    ]
                )
            }
        }
    }
}