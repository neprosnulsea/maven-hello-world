pipeline {

    tools {
        jdk 'JDK_8u221'
        jdk 'JDK_8u60'
        maven 'Maven 3.6.3'
        maven 'Maven 3.0.5'
    }


    stages { 
       
         stage('Get App Source Code') {
            steps {
                echo "===================== CLONE PROJECT'S SOURCE CODE ====================="
                checkout([
                    $class: 'GitSCM',
                    doGenerateSubmoduleConfigurations: false,
                    userRemoteConfigs: [[
                    url: 'https://bitbucket.endava.com/scm/jjmt/java-migration-test.git',
                    credentialsId: "19921a88-81f3-4684-898a-80aba717b08b"
                    ]],
                    branches: [ [name: '*/master'] ]
                ])
            }
        }

         stage('Build maven') { 
            steps { 

                echo "===================== MAVEN BUILD ====================="

                dir('maven-hello-world-master/my-app'){
                    sh 'mvn package -DskipTests=true'
                }
            }
        }

           stage('SonarQube analysis') {
             steps {
                 echo "===================== SONARQUBE ANALYSIS ====================="

                 dir('maven-hello-world-master/my-app'){
                     script {

                             withSonarQubeEnv('New Sonar Endava') {
                                 sh 'mvn sonar:sonar ' +
                                 //'-Dsonar.sources=. ' +
                                 '-Dsonar.projectKey=JMT ' +
                                 '-Dsonar.login=72d6a54735e8e9d91dbc3448eaeafcf4366b8923 ' +
                                 '-Dsonar.java.binaries=. ' +
                                 '-DskipTests=true' +
                                 '-Dsonar.cfamily.build-wrapper-output=bw-output ' +
                                 '-Dsonar.projectName="Java Migration Test" ' +
                                 '-Dsonar.projectVersion=$BUILD_NUMBER'
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
