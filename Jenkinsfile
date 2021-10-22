pipeline {
    agent any 
    stages {
        stage('Checkout') { 
            steps {
                echo 'Making copy source code from GIT repository'
                //sh '''
                   //git clone https://github.com/neprosnulsea/maven-hello-world.git
                //'''
            }
        }
        stage('Build') { 
            steps {
                echo 'Compiling code'
                sh '''
                mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
                cd my-app
                mvn compile
                java -cp target/classes com.mycompany.app.App
                mvn clean --quiet
                ack -a -f
                pom.xml
                src/main/java/com/mycompany/app/App.java
                src/test/java/com/mycompany/app/AppTest.java
                '''
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying application'
            }
        }
    }
}
