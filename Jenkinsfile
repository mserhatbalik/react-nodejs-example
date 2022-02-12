pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'building the docker image..'
                  withCredentials([usernamePassword(credentialsId: 'nexus-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t 188.166.153.139:8083/react-node-js-app:1.1 .'
                    sh "echo $PASS | docker login -u $USER --password-stdin 188.166.153.139:8083"
                    sh 'docker push 188.166.153.139:8083/react-node-js-app:1.1'
                  }
            }
        }
    }
}