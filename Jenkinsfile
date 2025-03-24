pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
        stage('Manual Approval') {
            steps {
                script {
                    def userInput = input(
                        message: 'Lanjutkan ke tahap Deploy?',
                        parameters: [
                            choice(name: 'Pilihan', choices: ['Proceed', 'Abort'], description: 'Pilih apakah akan melanjutkan ke tahap Deploy atau tidak.')
                        ]
                    )
                    if (userInput == 'Abort') {
                        error("Pipeline dihentikan oleh pengguna.")
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'npm start &'
                sleep 60
                sh 'pkill -f "node"'
            }
        }
    }
}

