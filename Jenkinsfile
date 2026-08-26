pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Image') {
            steps {
                script {
                    sh 'docker build -t team-skeleton:${BUILD_NUMBER} .'
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
        }
    }
    
    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        success {
            echo "Environment check passed: Maven, JDK, and JUnit are installed and working."
        }
        failure {
            echo "Environment check failed — see console output for the missing/broken tool."
        }
    }
}