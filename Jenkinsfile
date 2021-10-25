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
           // mvn clean verify sonar:sonar -Dsonar.login=myAuthenticationToken
           bash 'mvn sonar:sonar -Dsonar.host.url=http://127.0.0.1:9000'
           -Dsonar.login=the-generated-token
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
