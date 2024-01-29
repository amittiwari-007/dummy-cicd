pipeline {
    agent any

     environment {
        SSH_KEY = credentials('ssh-key')
    }

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
                echo "builded"
                archiveArtifacts 'build/**'
            }
        }

        stage('Deploy to Azure VM') {
            steps {
                script {
                     def remoteHost = '192.168.1.6'
                def remoteUser = 'root'
                def remotePwd = '6P@ssw0rd6'
                def remoteDir = '/root/home/Dhanush/dummy/'
                
                echo "outside"
                    withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key', keyFileVariable: 'SSH_KEY')]) {
                        echo "inside"
                        sh 'scp -r -i $SSH_KEY build/* root@192.168.1.6:/root/home/Dhanush/dummy'
                    }
                
                }
            }
        }
        
    }
}
