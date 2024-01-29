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
                    withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key')]) {
                // sshagent(['ssh-key']) {
                    echo "inside"
                    sh """
        ssh-add -L
        ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -p ${remotePort} ${remoteUser}@${remoteHost} "echo Successfully connected"
        scp -o StrictHostKeyChecking=no -r build/* ${remoteUser}@${remoteHost}:${remoteDir}

    """
                }
                }
            }
        }
        
    }
}
