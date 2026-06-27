pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --no-restore --configuration Release'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'dotnet test --no-build --configuration Release --verbosity normal'
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully — all tests passed.'
        }
        failure {
            echo 'Pipeline failed — check the build or test output above.'
        }
    }
}
