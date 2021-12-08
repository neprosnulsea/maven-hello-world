pipeline {
    agent any
    tools {
        maven 'maven'
    }

    stages {
        stage('Clone source from Github') {
            steps {
                git branch: 'master',
                url: 'https://github.com/neprosnulsea/maven-hello-world.git'
                checkout scm  
            }
        }
        stage('Maven Build') {
            tools{
                jdk 'jdk8'
            }
            steps {
                sh 'mvn install'
            }
        }
        stage('SonarQube') {
            tools{
                jdk 'jdk11'
            }
        environment {
            scannerHome = tool 'SonarQube Scanner'
        } 
        steps {
        withSonarQubeEnv(installationName: 'SonarQube') {
            sh '''
                mvn clean verify sonar:sonar \
  -Dsonar.projectKey=maven-hello-world \
  -Dsonar.host.url=http://172.23.160.41:9000 \
  -Dsonar.login=540ad239c770ad427d4a50196dbd4bf8a2421fed \
  -Dsonar.sources=. \
  -Dsonar.java.binaries=. 
            
            '''
            }   
        }

    }
}
}
