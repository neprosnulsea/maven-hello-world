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
           mvn clean verify sonar:sonar -Dsonar.login=bcb0b1d3131b45c7d06f44f5d9d57bdf1f9d3c0c
           mvn sonar:sonar -Dsonar.host.url=http://127.0.0.1:9000
           -Dsonar.login=bcb0b1d3131b45c7d06f44f5d9d57bdf1f9d3c0c
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
