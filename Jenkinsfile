pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
              dir('/home/michell/Documentos/Diplomado/ejemplo-maven/'){
                sh './mvnw clean compile -e'
              }
            }
        }
        stage('Unit') {
            steps {
              dir('/home/michell/Documentos/Diplomado/ejemplo-maven/'){
                sh './mvnw clean test -e'
              }
            }
        }
        stage('Jar') {
            steps {
              dir('/home/michell/Documentos/Diplomado/ejemplo-maven/'){
                sh './mvnw clean package -e'
              }
            }
        }
        stage('Run') {
            steps {
              dir('/home/michell/Documentos/Diplomado/ejemplo-maven/'){
                sh 'nohup bash mvnw spring-boot:run &'
                sh 'sleep 20'
              }
            }
        }
        stage('Test') {
            steps {
              dir('/home/michell/Documentos/Diplomado/ejemplo-maven/'){
                sh 'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing"'
                sh 'curl -X GET "http://localhost:8081/rest/mscovid/estadoPais?pais=VE"'
                sh 'curl -X GET "http://localhost:8081/rest/mscovid/estadoMundial"'              }
            }
        }
    }
}