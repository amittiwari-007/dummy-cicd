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
                archiveArtifacts 'dist/**'
            }
        }

        // stage('Debug') {
        //     steps {
        //         script {
        //             bat 'echo Workspace: %WORKSPACE%'
        //             bat 'echo Contents of dist directory: '
        //             bat 'dir dist'
        //             bat 'echo Files in dist directory: && dir /B /A-D /S dist'
        //             bat 'echo Directories in dist directory: && dir /B /A:D /S dist' 
        //         }

        //     }
        // }


        stage('Deploy to Azure VM') {
            steps {
                script {
                     def remoteHost = '192.168.1.6'
                def remoteUser = 'root'
                def remotePwd = '6P@ssw0rd6'
                def remoteDir = '/root/home/Dhanush/dummy/'
                
                echo "outside"
                   // withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key', keyFileVariable: 'SSH_KEY')]) {
                        echo "inside"
                        echo "SSH_KEY: ${SSH_KEY}"
                        bat 'scp -r -i %SSH_KEY% %WORKSPACE%\\dist\\* root@192.168.1.6:/home/Dhanush/dummy'
                    echo "done bhai connect to ho hi gaya 
                  //  }
                
                }
            }
        }
        
    }
}
