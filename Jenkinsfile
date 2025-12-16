pipeline {
    agent { label 'linux' }

    tools {
        jdk 'Java17'
        maven 'Maven3'
    }

    options {
        timestamps()
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Check Agent & Tools') {
            steps {
                sh '''
                    set -e
                    echo "===== Agent Details ====="
                    hostname
                    whoami

                    echo "===== Java Version ====="
                    java -version

                    echo "===== Maven Version ====="
                    mvn -version
                '''
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build (Compile)') {
            steps {
                sh '''
                    set -e
                    mvn clean compile
                '''
            }
        }

        stage('Run Java App') {
            steps {
                sh '''
                    set -e
                    mvn exec:java -Dexec.mainClass=HelloWorld
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully on Linux agent 🚀"
        }
        failure {
            echo "❌ Pipeline failed. Check logs for details."
        }
        always {
            echo "Pipeline finished."
        }
    }
}
