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
            //mvn clean verify sonar:sonar
           // mvn clean verify sonar:sonar -Dsonar.login=94cbfff18355c9d3d09b4d9a2379ec356db16c8d -Dsonar.host.url=http://192.168.0.37:9000 -Dsonar.projectKey=project -Dsonar.projectName=Hello_world_Maven_SonarQube -Dsonar.sourceEncoding=UTF-8 -Dsonar.language=java -Dsonar.sources=project/src/main -Dsonar.tests=project/src/test
          mvn verify sonar:sonar 
          -Dsonar.sources=.
          -Dsonar.host.url=http://192.168.0.37:9000
          //-Dsonar.login=94cbfff18355c9d3d09b4d9a2379ec356db16c8d
          -Dsonar.login=admin
          -Dsonar.password=123123
          -Dsonar.projectKey=Hello_world_Maven_SonarQube
          -Dsonar.java.binaries=. 
          -DskipTests=true
          -Dsonar.cfamily.build-wrapper-output=bw-output 
          -Dsonar.projectName=Hello_world_Maven_SonarQube
          -Dsonar.projectVersion=$BUILD_NUMBER
          '''
         }
       } 
    //stage('SonarQube_Analysis') {
      //steps {
    //withSonarQubeEnv() {
      //sh "${maven}/bin/mvn clean verify sonar:sonar"
      //sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar -P sonar -Dsonar.host.url=http://192.168.0.37:9000 -Dsonar.jdbc.url=$SONAR_JDBC_URL -Dsonar.jdbc.username=$SONAR_JDBC_USERNAME -Dsonar.jdbc.password=$SONAR_JDBC_PASSWORD'
    //}
      //}
  //}
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
