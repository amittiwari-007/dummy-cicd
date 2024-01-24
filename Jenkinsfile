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

        stage('Deploy to Azure VM') {
            steps {
                script {
                    // Use SSH to copy artifacts to Azure VM
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: 'Dummy',
                                transfers: [
                                    sshTransfer(
                                        cleanRemote: true,
                                        excludes: '',
                                        execCommand: '',
                                        execTimeout: 120000,
                                        flatten: false,
                                        makeEmptyDirs: false,
                                        noDefaultExcludes: false,
                                        patternSeparator: '[, ]+',
                                        remoteDirectory: '/home/Dhanush/dummy',
                                        remoteDirectorySDF: false,
                                        removePrefix: 'build/',
                                        sourceFiles: 'C:/Users/Amit.Tiwari/OneDrive - Tolaram Corporation Pte Ltd/Desktop/dummy/my-react-app/build/**/*'
                                    )
                                ],
                                usePromotionTimestamp: false,
                                useWorkspaceInPromotion: false,
                                verbose: true
                            )
                        ]
                    )
                }
            }
        }
        
    }
}
