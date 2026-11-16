
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting latest GitHub code'
                checkout scm
            }
        }

        stage('Check Requirements') {
            steps {
                bat 'type requirements.txt'
            }
        }

        stage('Install Requirements') {
            steps {
                bat 'py -m pip install -r requirements.txt'
            }
        }

        stage('Build') {
            steps {
                bat 'py -m py_compile app.py'
                echo 'Build successful'
            }
        }

        stage('Run Application') {
            steps {
                bat 'py app.py'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Pipeline completed'
        }

        failure {
            echo 'ERROR: Pipeline failed'
        }
    }
}
