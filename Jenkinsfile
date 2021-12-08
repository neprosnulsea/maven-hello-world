pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk8'
          }
    stages {
        stage('Clone code from GitHub') {
            steps {
                git branch: 'master',
                url: 'https://github.com/neprosnulsea/maven-hello-world.git'
                checkout scm  
            }
        }
        stage('Build the code') {
            steps {
                echo "===================== MAVEN BUILD ====================="
                //sh 'mvn install'
                sh 'mvn package -DskipTests=false'
            }
        }
        stage('Scan the code via Sonar') {
            tools{
                jdk 'jdk11'
            }
        steps {
            sh '''
                echo "===================== SONARQUBE ANALYSIS ====================="
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
