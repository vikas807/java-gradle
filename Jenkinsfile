pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '2de63975-c69e-423b-9ba1-8d53b5619dda', url: 'https://github.com/vikas807/java-maven.git']]])
            sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t vikas807/my-app-1.0 .'
                }
            }
        }
         stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'vikas807', variable: 'Dockerhubpwd')]) {
                    sh 'docker login -u vikas807 -p ${Dockerhubpwd}'
}
                
                    sh 'docker push vikas807/my-app-1.0'
                }
            } 
         }
    }
}