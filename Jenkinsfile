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
                mvn compile
                java -cp target/classes com.mycompany.app.App
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
