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
         stage('Scan') {
            steps {
                 withSonarQubeEnv(installationName: 'Sonar1') {
                     sh 'mvn clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1:sonar'
                 }
            }
        }
        stage('Docker Build') {
            steps {
	        sh 'find .'
                sh 'docker build -t springboot_hello:latest -f Dockerfile .'
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
