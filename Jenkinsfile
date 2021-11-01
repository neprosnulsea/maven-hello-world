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
                                    -Dsonar.projectKey=Hello_world_Maven_SonarQube \
                                    -Dsonar.host.url=http://127.0.0.1:9000 \
                                    -Dsonar.login=06c56e61f9bd67b6502145f5a249bcc23b31610f \
                                    -Dsonar.password=123123 \
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
