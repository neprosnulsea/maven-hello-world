pipeline {
  agent any
  tools {
      maven 'MAVEN'
      jdk "jdk11"
    }
  stages {
      stage("Build") {
          steps {
          echo 'STARTING BUILD'
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/neprosnulsea/maven-hello-world.git']]])
          sh "mvn -Dmaven.test.failure.ignore=true clean package"
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
