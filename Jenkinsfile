pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    
                    bat 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }
        
    }
}
