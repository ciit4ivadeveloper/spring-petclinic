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

    stage('Docker Build') {
      steps {
        withMaven(maven : 'mvn-3.5.0') {
           sh 'docker build -t grupo04/spring-petclinic:latest .'
        }
      }
    } 

    stage('Junit') {
      steps {
        withMaven(maven : 'mvn-3.5.0') {
           sh 'mvn clean compile test'
        }
      }
    }
    
    stage('SonarQube analysis') {
      steps {
        withSonarQubeEnv(credentialsId: 'sonarqube-secret', installationName: 'sonarqube-server') {
          withMaven(maven : 'mvn-3.5.0') {
            sh 'mvn sonar:sonar -Dsonar.dependencyCheck.jsonReportPath=target/dependency-check-report.json -Dsonar.dependencyCheck.xmlReportPath=target/dependency-check-report.xml -Dsonar.dependencyCheck.htmlReportPath=target/dependency-check-report.html -Dsonar.java.pmd.reportPaths=target/pmd.xml -Dsonar.java.spotbugs.reportPaths=target/spotbugsXml.xml -Dsonar.zaproxy.reportPath=target/zap-reports/zapReport.xml -Dsonar.zaproxy.htmlReportPath=target/zap-reports/zapReport.html'
          }
        }
      }
    }

    
  }
}
