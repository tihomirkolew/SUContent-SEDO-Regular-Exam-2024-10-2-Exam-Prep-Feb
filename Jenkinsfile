pipeline {
    agent any

    // Trigger the pipeline only for the feature-ci-pipeline branch
    environment {
        BRANCH_NAME = 'feature-ci-pipeline'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'feature-ci-pipeline') {
                        checkout scm
                    } else {
                        error "This pipeline only runs on the 'feature-ci-pipeline' branch."
                    }
                }
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
