pipeline {
    agent any 
    stages {
        stage('Checkout') { 
            steps {
                echo 'Making copy source code from GIT repository'
                //sh 'git clone https://github.com/neprosnulsea/maven-hello-world.git'
            }
        }
        stage('Build') { 
            steps {
                echo 'Compiling code'
                sh '''
                cd my-app
                mvn package
                java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App
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
