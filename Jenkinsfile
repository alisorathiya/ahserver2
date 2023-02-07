pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 1, unit: 'SECONDS')
    }
    stages {
        stage('build') {
            steps {
             echo 'Building Application...'
            }
        }
         stage('test') {
            steps {
             echo 'Testing Application...'
            }
        }
         stage('deploy') {
            steps {
             echo 'Deploying Application...'
            }
        }
    }
}
