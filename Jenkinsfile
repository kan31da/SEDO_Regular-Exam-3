pipeline {
    agent any

    triggers {       
        pollSCM('* * * * *') 
    }

    stages {
        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build Application') {
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Run Unit and Integration Tests') {
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        success {
            echo '✅ Build and tests successful!'
        }
        failure {
            echo '❌ Build or tests failed.'
        }
    }
}