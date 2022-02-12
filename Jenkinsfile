pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                echo 'building the docker image..'
                  withCredentials([usernamePassword(credentialsId: 'nexus-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t 188.166.153.139:8083/react-node-js-app:1.2 .'
                    sh "echo $PASS | docker login -u $USER --password-stdin 188.166.153.139:8083"
                    sh 'docker push 188.166.153.139:8083/react-node-js-app:1.2'
                  }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def dockerCmd = 'docker run -p 3080:3080 -d 188.166.153.139:8083/react-node-js-app:1.2'
                    sshagent(['ec2-test-credentials']) {
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@3.71.175.216 ${dockerCmd}"
                    }
                }
            }
        }
    }
}