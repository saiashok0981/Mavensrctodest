pipeline {
    agent any

    tools {
        maven 'Maven'     // Use the actual name configured in Jenkins
        jdk 'JDK'         // Use the actual name configured in Jenkins
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
                // Automatically run the generated jar
                sh 'java -jar $(find target -type f -name "*.jar" ! -name "*original*" | head -n 1)'
            }
        }
    }

    post {
        success {
            echo 'Build and execution succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
