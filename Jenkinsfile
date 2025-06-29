pipeline {
    agent any
	tools {
        dotnetsdk 'dotnet-sdk-8.0'
    }
    stages {
		stage ('Checkout') {
			steps { 
				checkout scm
			}
		}
        stage('Restore the project') {
            steps {
                bat 'dotnet restore'
            }
        }
        stage('Build the project') {
            steps {
                bat 'dotnet build --no-restore'
            }
        }
        stage('Test the project') {
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}