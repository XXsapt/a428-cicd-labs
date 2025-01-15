pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '--privileged --env DOCKER_TLS_CERTDIR= '
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'node --version'
            }
        }
    }
}