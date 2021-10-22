pipeline {
    agent any 
    stages {
        stage('Checkout') { 
            steps {
                echo 'Making copy source code from GIT repository'
                sh 'git clone https://github.com/neprosnulsea/maven-hello-world.git'
            }
        }
        stage('Test') { 
            steps {
                echo 'Testing application'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying application'
            }
        }
    }
}
