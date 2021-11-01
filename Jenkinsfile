pipeline {
  agent any
  tools {
        jdk 'jdk'
        maven 'Maven'
    }
  stages {
      stage('Get App Source Code') 
      {
        steps {
                echo "CLONE CODE FROM GIT"
                checkout([
                  $class: 'GitSCM', 
                  branches: [[name: '*/master']], 
                  extensions: [], 
                  userRemoteConfigs: [[url: 'https://github.com/neprosnulsea/maven-hello-world.git']]])
              }
      }

      stage('Build maven') { 
        steps { 
                echo "BUILD MAVEN"
                    sh 'mvn package -DskipTests=true'
            }
        }

       stage('SonarQube analysis') {
             steps {
                 echo "Sonar Analys"
                     script {
                                 sh '''
                                    mvn clean verify sonar:sonar \
                                    -Dsonar.projectKey=maven-hello-world \
                                    -Dsonar.host.url=https://sonarcloud.io \
                                    // -Dsonar.password=123123 \
                                 '''
                       }
             }
         }
  }

post { 
        always { 
            cleanWs()
        }
    }
}
