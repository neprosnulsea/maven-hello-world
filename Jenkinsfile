pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk8'
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
            steps {
                sh 'mvn install'
            }
        }
        stage('SonarQube') {
            tools{
                jdk 'jdk11'
            }
        environment {
            scannerHome = tool 'sonar'
        } 
        steps {
        withSonarQubeEnv(installationName: 'sonar') {
                                 sh '''
                                    mvn clean verify sonar:sonar \
                                    -Dsonar.projectKey=Hello_world_Maven_SonarQube \
                                    -Dsonar.host.url=http://172.27.160.1:9000 \
                                    -Dsonar.login=540ad239c770ad427d4a50196dbd4bf8a2421fed
                                 '''
            }   
        }

    }
}
}
