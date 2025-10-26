pipeline {
    agent any

    triggers {       
        pollSCM('* * * * *')
    }

    stages {
        stage('Build Application') {
            when {
                branch 'main'
            }
            steps {
                bat 'dotnet build'
            }
        }

        stage('Run Unit and Integration Tests') {
            when {
                branch 'main'
            }
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