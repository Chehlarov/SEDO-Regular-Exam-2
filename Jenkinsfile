pipeline {
    agent any

    tools {
        dotnetsdk 'dotnet-sdk-8.0'  // Requires Jenkins .NET SDK tool configuration
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Restore') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet restore'
                    } else {
                        bat 'dotnet restore'
                    }
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet build --no-restore'
                    } else {
                        bat 'dotnet build --no-restore'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet test --no-build --verbosity normal'
                    } else {
                        bat 'dotnet test --no-build --verbosity normal'
                    }
                }
            }
            post {
                always {
                    junit '**/TestResults/*.trx'  // Publish test results
                }
            }
        }
    }
}
