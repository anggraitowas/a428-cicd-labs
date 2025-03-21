node {
    // Menentukan Docker image dan argumen untuk container
    def customDockerImage = 'node:16-buster-slim'
    def dockerArgs = '-p 3000:3000'

    try {
        // Stage Build: Menjalankan npm install di dalam Docker container
        stage('Build') {
            echo 'Running npm install in Docker container...'
            docker.image(customDockerImage).inside(dockerArgs) {
                sh 'npm install'  // Menginstal dependensi menggunakan npm
            }
        }

        // Stage Test: Menjalankan script test.sh di dalam Docker container
        stage('Test') {
            echo 'Running test script in Docker container...'
            docker.image(customDockerImage).inside(dockerArgs) {
                sh './jenkins/scripts/test.sh'  // Menjalankan skrip test.sh
            }
        }

    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}

