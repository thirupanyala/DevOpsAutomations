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
        success {
            mail to: 'thirupanyla2k2@gmail.com',
                 subject: "Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Great news! The build succeeded for ${env.JOB_NAME} #${env.BUILD_NUMBER}.\nCheck details: ${env.BUILD_URL}"
        }    
        failure {
            mail to: 'ptreddy2016@gmail.com',
                 subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed for ${env.JOB_NAME} #${env.BUILD_NUMBER}.\nCheck details: ${env.BUILD_URL}"
        }
    }
}
