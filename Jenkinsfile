pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Rohan-kate123/apachewe.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Artifacts') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t netflix2 .'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy(
                    adapters: [
                        tomcat9(
                            credentialsId: 'jenkins',
                            url: 'http://13.203.203.183:8080'
                        )
                    ],
                    contextPath: 'netflix',
                    war: 'target/*.war'
                )
            }
        }
    }
}
