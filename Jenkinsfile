pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'     // Use the name defined in Jenkins -> Global Tool Configuration
        jdk 'OpenJDK 11'        // Adjust to your configured JDK version
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
                // Automatically run the generated jar file (ignores original-jar or test-jars)
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
