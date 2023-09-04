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
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBackend -Dsonar.host.url=http://192.168.1.178:9000 -Dsonar.login=sqp_793b439115b4d752ff11bf59434ed693ad3d7abb -Dsonar.java.binaries=target"

                }
            }
        }
        stage ('Quality Gate') {
            steps {
                sleep(5)
                timeout(time: 1, unit:'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage ('Deploy Backend') {
            steps {
                sh 'echo NotRunning!'
                sh 'apt update -y'
                // deploy adapters: [tomcat9(credentialsId: 'TomCatLogin', path: '', url: 'http://192.168.1.174:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }
        stage ('End Message') {
            steps {
                dir('frontend'){
                    input message: 'Finishing deployment...Send report message?'
                    // git url: 'https://github.com/LFDM-85/tasks-frontend'
                    // sleep(1)
                    // sh 'mvn clean package'
                    // deploy adapters: [tomcat9(credentialsId: 'TomCatLogin', path: '', url: 'http://192.168.1.174:8001/')], contextPath: 'tasks', war: 'target/task.war'
                }
            }
        }
    }
}


