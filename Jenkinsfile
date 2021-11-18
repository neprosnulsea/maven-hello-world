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
                       withSonarQubeEnv('sonar') {
                                 sh '''
                                    mvn clean verify sonar:sonar \
                                    -Dsonar.projectKey=Hello_world_Maven_SonarQube \
                                    -Dsonar.host.url=http://172.27.160.1:9000 \
                                    -Dsonar.login=540ad239c770ad427d4a50196dbd4bf8a2421fed
                                 '''
                     }
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
