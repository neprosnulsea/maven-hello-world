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
       sh '''
       mvn clean verify sonar:sonar -Dsonar.login=myAuthenticationToken
       '''
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
