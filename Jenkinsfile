pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('SonarQube Analysis') {           
            
            steps {
                echo 'not running for now'
            }
        }
    }
}


