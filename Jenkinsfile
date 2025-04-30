pipeline {
    agent any

    tools {
        maven 'Maven'     // Adjust as per Jenkins tool config
        jdk 'JDK'         // Adjust as per Jenkins tool config
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

        stage('Debug: List Target Folder') {
            steps {
                sh 'ls -lh target'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Run Application') {
            steps {
                script {
                    def jarFile = sh(script: 'find target -type f -name "*-jar-with-dependencies.jar" | head -n 1', returnStdout: true).trim()
                    if (jarFile == "") {
                        error("❌ Could not find fat JAR file!")
                    }
                    sh "java -jar ${jarFile}"
                }
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
