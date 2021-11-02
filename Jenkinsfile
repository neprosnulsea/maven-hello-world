pipeline {
  agent any
  tools {
        jdk 'jdk'
        maven 'maven'
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
          dir('maven-hello-world/my-app') {
                    sh 'mvn package -DskipTests=true'
                }
                }
        }

       stage('SonarQube analysis') {
             steps {
                 echo "Sonar Analys"
                     script {
                                 sh '''
                                    mvn clean verify sonar:sonar
                                    mvn clean verify sonar:sonar -Dsonar.login=9ba97ca33379c21d31ce38f43e631bbaa21d03bf
  -Dsonar.projectKey=maven-hello-world1 \
  -Dsonar.host.url=http://172.27.160.1:9000 \
  -Dsonar.login=9ba97ca33379c21d31ce38f43e631bbaa21d03bf
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
