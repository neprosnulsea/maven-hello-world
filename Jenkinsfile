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
          dir('maven-hello-world-master/my-app') {
                    sh 'mvn package -DskipTests=true'
                }
                }
        }

       stage('SonarQube analysis') {
             steps {
                 echo "Sonar Analys"
               dir('maven-hello-world-master/my-app') {
                     script {
                                 sh '''
                                    mvn clean verify sonar:sonar -Dsonar.login=9ba97ca33379c21d31ce38f43e631bbaa21d03bf
                                    mvn clean verify sonar:sonar \
                                    -Dsonar.projectKey=Hello_world_Maven_SonarQube \
                                    -Dsonar.host.url=http://127.0.0.1:9000 \
                                    -Dsonar.login=28445b7ca0a6dee74ea1bb9c4d67e6f550cfc4f2
                                 '''
                       }
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
