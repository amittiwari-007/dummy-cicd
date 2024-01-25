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
                
                echo "yaha"
                sshagent(credentials: ['5823f776-71c3-453b-bd45-9a2514aee17c']) {
                    
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
