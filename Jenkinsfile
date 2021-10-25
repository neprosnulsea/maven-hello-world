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
           // mvn clean verify sonar:sonar
           chown -R jenkins /var/jenkins_home/workspace/Hello_world_Maven_SonarQube@tmp/durable-0bb511eb/
           mvn clean verify sonar:sonar -Dsonar.login=myAuthenticationToken -Dsonar.host.url=http://192.168.0.37:9000 -Dsonar.projectKey=project -Dsonar.projectName=Hello_world_Maven_SonarQube -Dsonar.sourceEncoding=UTF-8 -Dsonar.language=java -Dsonar.sources=project/src/main -Dsonar.tests=project/src/test
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
