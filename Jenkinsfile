pipeline {
  agent { label 'GOL' }

  triggers { pollSCM ('* * * * *') }

  stages {
    stage('SCM') {
      steps {
        git branch: 'qa', url: 'https://github.com/AnasAnsar1/spring-petclinic.git'
      }
    }

    stage('Build & Sonar Analysis') {
      steps {
        withSonarQubeEnv('SELF_HOSTED') {
          sh 'mvn clean package sonar:sonar'
      }
      }
    }
  }

}