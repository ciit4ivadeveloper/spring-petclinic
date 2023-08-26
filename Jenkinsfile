#!groovy

pipeline {
  agent any
  environment {
      // Definir variables de entorno para la configuración de SonarQube
      SONAR_HOST_URL = credentials('http://172.17.0.4:9000') // Credencial de URL de SonarQube
      SONAR_LOGIN = credentials('02ade3e1025b7188495e01483bd317be0cc74dec') // Credencial de token de acceso a SonarQube
  }
  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3.5.0'
        }
      }
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t grupo04/spring-petclinic:latest .'
      }
    }
    stage('SonarQube analysis') {
      agent any
      steps {
        withSonarQubeEnv(credentialsId: 'sonarqube-secret', installationName: 'sonarqube-server') { 
            sh 'mvn sonar:sonar'
          }
      } 
    } 
  }
}
