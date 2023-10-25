pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
    post {
        failure {
            emailext (
                subject: "Build Failed",
                body: "The build has failed. Please check the Jenkins build log.",
                recipientProviders: [[$class: 'CulpritsRecipientProvider']],
                to: 'restrella@77global.biz'
            )
        }
        success {
            emailext (
                subject: "Build Successful",
                body: "The build has completed successfully.",
                recipientProviders: [[$class: 'CulpritsRecipientProvider']],
                to: 'restrella@77global.biz'
            )
        }
    }
}