

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Build your project here
                sh 'ls'
                sh 'pwd'
                
                // Stash the file(s) you want to move to the artifacts folder
                stash includes: 'andres.txt', name: 'myStash'
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
                                sshTransfer(sourceFiles: "andres.txt",)
                            ]
                        )
                    ]
                )
            }
        }

    }

    post {
        always {
            // Unstash the file(s) from the stash and move them to the artifacts folder
            unstash 'myStash'
            archiveArtifacts artifacts: '/home/ec2-user/andres.txt', fingerprint: true
        }
    }
}