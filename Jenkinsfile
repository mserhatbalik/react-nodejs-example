pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'building the docker image..'
                  withCredentials([usernamePassword(credentialsId: 'nexus-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t 64.227.37.27/react-node-js-app:1.0 .'
                    sh "echo $PASS | docker login -u $USER --password-stdin 64.227.37.27:8083"
                    sh 'docker push 64.227.37.27:8083/react-node-js-app:1.0'
                  }
            }
        }
}