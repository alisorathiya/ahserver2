pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 1, unit: 'SECONDS')
    }
    stages {
        stage('Build') {
            steps {
             echo 'Building Application...'
            }
        }
         stage('Test') {
            steps {
             echo 'Testing Application...'
            }
        }
         stage('Deploy') {
            steps {
             echo 'Deploying Application...'
            }
        }
    }
}
