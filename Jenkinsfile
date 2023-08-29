pipeline {
  agent any

  tools {
    jdk 'jdk-11'
    maven 'mvn-3.5.0'
  } 

  stages {
    stage('Maven Install') {
      steps {
        withMaven(maven : 'mvn-3.5.0') {
           sh 'mvn clean install'
        }
      }
    }
    
    stage('Build') {
      steps {
        withMaven(maven : 'mvn-3.5.0') {
           sh 'docker build -t grupo04/spring-petclinic:latest .'
        }
      }
    } 
  }
}
