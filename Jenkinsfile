pipeline {
    agent { label 'linux' }

    tools {
        jdk 'Java17'
        maven 'Maven3'
    }

    stages {

        stage('Check Agent') {
            steps {
                sh '''
                  echo "Running on Jenkins Agent:"
                  hostname
                  whoami
                  java -version
                  mvn -version
                '''
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Run Java App') {
            steps {
                sh '''
                  javac src/main/java/HelloWorld.java
                  java -cp src/main/java HelloWorld
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully on agent 🚀"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
