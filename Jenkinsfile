pipeline {
    agent any
    
    tools {
        maven 'Maven'
    }

    stages {
        stage('Pull Code') {
            steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/jglick/simple-maven-project-with-tests.git'
                cleanWs()
                //checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']])
                //checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/in28minutes/spring-boot-examples.git']])
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/senthilamigo/spring-boot-deploy.git']])
            }
        }
         stage('Build') {
            steps {
                sh 'mvn --version'
                sh 'mvn clean install'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot_hello:latest .'
            }
       }
    }
    post {
        always {
            //cleanWS()
             echo 'I will always say Hello!'
        }
    }
}