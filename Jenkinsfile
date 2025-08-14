pipeline {
    agent none
    stages {
        stage('Build Java with Maven') {
            agent {
                docker { image 'maven:3.8.1-adoptopenjdk-11' }
            }
            steps {
                dir('backend') {
                    sh 'mvn clean install'
                }
            }
        }
        stage('Run Java App') {
            agent {
                docker { image 'openjdk:11' }
            }
            steps {
                dir('backend') {
                    sh 'java -cp target/hello-world-backend-1.0-SNAPSHOT.jar com.example.App'
                }
            }
        }
        stage('Build Node App') {
            agent {
                docker { image 'node:16-alpine' }
            }
            steps {
                dir('frontend') {
                    sh 'npm install'
                }
            }
        }
        stage('Run Node App') {
            agent {
                docker { image 'node:16-alpine' }
            }
            steps {
                dir('frontend') {
                    sh 'npm start'
                }
            }
        }
    }
}
