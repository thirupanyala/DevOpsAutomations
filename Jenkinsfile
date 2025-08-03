pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout current branch for multibranch pipeline
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // Build Maven multi-module project
                sh 'mvn -B clean compile'
            }
        }
        stage('Test') {
            steps {
                // Run tests and collect results
                sh 'mvn -B test'
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
