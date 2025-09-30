pipeline {
    agent any
    
    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/la3mor/student-management.git'
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
        
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    
    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        success {
            echo '✅ Build réussi! Tests passés avec H2 database.'
        }
        failure {
            echo '❌ Build échoué! Vérifiez les logs.'
        }
    }
}
