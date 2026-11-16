
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
                echo 'Checking requirements.txt'
                bat 'type requirements.txt'
            }
        }

        stage('Install Requirements') {
            steps {
                bat '''
                "C:\\Users\\ELCOT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m pip install -r requirements.txt
                '''
            }
        }

        stage('Build') {
            steps {
                bat '''
                "C:\\Users\\ELCOT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m py_compile app.py
                '''
                echo 'Build successful'
            }
        }

        stage('Run Application') {
            steps {
                bat '''
                "C:\\Users\\ELCOT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" app.py
                '''
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

        always {
            echo 'Pipeline execution finished'
        }
    }
}

