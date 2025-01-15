pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '--privileged -v $PWD:/workspace -w /workspace -p 3000:3000'
        }
    }
    stages {
        stage('Install Dependencies') { 
            steps {
                // Pastikan npm sudah dapat diakses
                sh 'npm install'
            }
        }
        stage('Build Application') {
            steps {
                // Ganti dengan perintah build yang relevan untuk aplikasi Anda
                sh 'npm run build'
            }
        }
        stage('Run Tests') {
            steps {
                // Ganti dengan perintah test yang relevan
                sh 'npm test'
            }
        }
    }
}
