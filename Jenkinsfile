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
            environment {
                scannerHome = tool 'sonarqube-scanner'
            }
            steps {
                withSonarQubeEnv('Sonar-local-test') {
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectkey=DeployBack -Dsonar.host.url=http://192.168.1.178:9000 -Dsonar.login=sqa_acef57bab51d28298b45ce91bd373f2fdeebeabb -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"

                }
            }
        }
    }
}


