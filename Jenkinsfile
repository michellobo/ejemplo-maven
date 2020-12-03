pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
              sh './mvnw clean compile -e'
            }
        }
        stage('Unit') {
            steps {
              sh './mvnw clean test -e'
            }
        }
        stage('Jar') {
            steps {
              sh './mvnw clean package -e'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }
        }
        stage('Run') {
            steps {
              sh 'nohup bash mvnw spring-boot:run &'
                sh 'sleep 20'
            }
        }
        stage('Test') {
            steps {
                sh 'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing"'
                sh 'curl -X GET "http://localhost:8081/rest/mscovid/estadoPais?pais=VE"'
                sh 'curl -X GET "http://localhost:8081/rest/mscovid/estadoMundial"' 
            }
        }
    }
}
