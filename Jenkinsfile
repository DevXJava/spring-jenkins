pipeline {
    agent any

    stages {
        stage('DEV Deployment') {
            steps {
                echo 'Starting DEV deployment...'
                build job: 'Dev'
            }
        }

        stage('UAT Deployment') {
            steps {
                echo 'Starting UAT deployment...'
                build job: 'UAT'
            }
        }

        stage('Production Approval') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    input(
                        message: 'Do you want to deploy this application to PRODUCTION?',
                        ok: 'Approve Production',
                        submitter: 'Dev'
                    )
                }
            }
        }

        stage('PROD Deployment') {
            steps {
                echo 'Starting PROD deployment...'
                build job: 'Prod'
            }
        }
    }

    post {
        success {
            echo 'All deployments completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        aborted {
            echo 'Pipeline was aborted or approval was rejected.'
        }
    }
}