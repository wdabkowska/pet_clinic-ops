pipeline {
    agent any

    tools {
        maven 'Maven'  // Configured in Jenkins global tool configuration as 'maven'
        jdk 'Java'     // Configured in Jenkins global tool configuration as 'java'
    }

    environment {
        // Defining JAVA_HOME may be optional, depending on your Jenkins configuration
        JAVA_HOME = tool 'Java'
    }


    stages {
        stage('Initialize') {
            steps {
                bat 'echo Pipeline started'
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/spring-projects/spring-petclinic.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                bat '.\\mvnw.cmd clean package'
            }
        }

        stage('Test') {
            steps {
                bat '.\\mvnw.cmd test'
            }

        post {
            always {
                junit 'target\\surefire-reports\\*.xml'
            }
        }
        }
    }
}
