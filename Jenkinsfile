pipeline {
    agent any

    tools {
        maven 'Maven'     // Replace with your actual Maven installation name in Jenkins
        jdk 'JDK'         // Replace with your actual JDK installation name in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: '42b7aada-7496-4388-bb42-97640354f8ff',
                    url: 'https://github.com/saiashok0981/Mavensrctodest.git'
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

        stage('Run Application') {
            steps {
                // Run the fat JAR with dependencies
                sh 'java -jar target/porna-1.0-SNAPSHOT-jar-with-dependencies.jar'
            }
        }
    }

    post {
        success {
            echo '✅ Build and execution succeeded!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
