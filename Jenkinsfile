#!groovy

pipeline {
  agent none
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
        withMaven(maven : 'mvn-3.6.3') {
            sh 'mvn sonar:sonar'
          }
      } 
    } 
  }
}
