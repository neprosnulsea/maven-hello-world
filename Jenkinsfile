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
       stage('Sonar') { 
         steps {
          sh '''
           mvn clean verify sonar:sonar
           -Dsonar.login=the-generated-token
           mvn clean install sonar:sonar
           // mvn clean install sonar:sonar -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=admin -Dsonar.password=123123 -X
          '''
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
