pipeline {
  agent any
  tools {
      maven 'MAVEN'
    }
  stages {
      stage('Build') {
          steps {
          echo 'STARTING BUILD'
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/neprosnulsea/maven-hello-world.git']]])
          sh "mvn -Dmaven.test.failure.ignore=true clean package"
          }
       }
       //stage('Sonar') { 
         //steps {
          //sh '''
           // mvn clean verify sonar:sonar
          // mvn clean verify sonar:sonar -Dsonar.host.url=http://192.168.0.37:9000 -Dsonar.projectKey=project -Dsonar.projectName=Hello_world_Maven_SonarQube -Dsonar.sourceEncoding=UTF-8 -Dsonar.language=java -Dsonar.sources=project/src/main -Dsonar.tests=project/src/test
         // '''
        // }
      // }
    stage('SonarQube analysis') {
      steps {
    withSonarQubeEnv(credentialsId: 'bcb0b1d3131b45c7d06f44f5d9d57bdf1f9d3c0c', installationName: 'My SonarQube Server') {
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    }
    }
  }
  }
 post {
       always {
          junit(
        allowEmptyResults: true,
        testResults: '*/test-reports/.xml'
      )
    }
}
}
