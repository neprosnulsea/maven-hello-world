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
            sh 'mvn sonar:sonar ' +
                '-Dsonar.host.url=http://172.27.160.1/:9000 ' +
                '-Dsonar.projectKey=project_test ' +
                '-Dsonar.login=540ad239c770ad427d4a50196dbd4bf8a2421fed ' +
                '-Dsonar.projectName=project_test ' +
                '-Dsonar.projectVersion=$BUILD_NUMBER'
            }   
        }

    }
}
}
