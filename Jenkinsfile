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
                echo "builded"
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
                // sshagent(['ssh-key']) {
                    echo "inside"
                     sh "scp -r -i $SSH_KEY build/* root@192.168.1.6:/root/home/Dhanush/dummy"
                }
                }
            }
        }
        
    }
}
