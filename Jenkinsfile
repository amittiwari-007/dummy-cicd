pipeline {
    agent any

    //  environment {
    //     SSH_KEY = credentials('ssh')
    // }

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
                archiveArtifacts 'dist/**'
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
                   withCredentials([sshUserPrivateKey(credentialsId: 'ssh', keyFileVariable: 'SSH_KEY')]) {
                        echo "inside"
                        echo "SSH_KEY: ${SSH_KEY}"
                        bat 'scp -r -B -i C:/Users/Amit.Tiwari/.ssh/id_ed25519 %WORKSPACE%\\dist\\* root@192.168.1.6:/home/Dhanush/dummy'
                    echo "done bhai connect to ho hi gaya "
                   }
                
                }
            }
        }
        
    }
}
