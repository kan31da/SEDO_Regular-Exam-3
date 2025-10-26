pipeline {
    agent any

    triggers {       
        pollSCM('* * * * *') 
    }

    stages {
        stage('Restore Dependencies') {
            when {
                expression { 
                    return env.GIT_BRANCH == 'origin/main' || env.BRANCH_NAME == 'main'
                }
            }
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build Application') {
            when {
                expression { 
                    return env.GIT_BRANCH == 'origin/main' || env.BRANCH_NAME == 'main'
                }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Run Unit and Integration Tests') {
            when {
                expression { 
                    return env.GIT_BRANCH == 'origin/main' || env.BRANCH_NAME == 'main'
                }
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