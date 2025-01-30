pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        // Kriteria 2: Tahap Build
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        // Kriteria 2: Tahap Test
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }

        // Kriteria 4: Tahap Manual Approval (Persetujuan Manual)
        stage('Manual Approval') {
            steps {
                script {
                    // Menampilkan dialog konfirmasi dengan pilihan Proceed/Abort
                    def userInput = input(
                        id: 'userInput',
                        message: 'Lanjutkan ke tahap Deploy?',
                        parameters: [
                            choice(
                                choices: ['Proceed', 'Abort'],
                                description: 'Pilih "Proceed" untuk melanjutkan atau "Abort" untuk membatalkan.',
                                name: 'approval'
                            )
                        ]
                    )
                    // Jika memilih Abort, hentikan pipeline
                    if (userInput == 'Abort') {
                        error("Pipeline dibatalkan oleh pengguna.")
                    }
                }
            }
        }

        // Kriteria 2: Tahap Deploy
        stage('Deploy') { 
            steps {
                // Kriteria 3: Menjalankan aplikasi, jeda 1 menit, lalu mengakhiri
                sh './jenkins/scripts/deliver.sh' 
                sh 'sleep 60' // Jeda 1 menit (Kriteria 3)
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}