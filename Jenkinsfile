def isMainBranch() {
    return env.GIT_BRANCH == 'origin/main' || env.BRANCH_NAME == 'main'
}

pipeline {
    agent any

    triggers {
        pollSCM('* * * * *') 
    }

    stages {
        stage('Restore Dependencies') {
            when { expression { isMainBranch() } }
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build Application') {
            when { expression { isMainBranch() } }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Run Unit and Integration Tests') {
            when { expression { isMainBranch() } }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        success { echo '✅ Build and tests successful!' }
        failure { echo '❌ Build or tests failed.' }
    }
}
