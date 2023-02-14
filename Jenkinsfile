pipeline {
    agent {label 'Master'}
    stages {
        stage('SCM') {
            steps{
                git branch: 'dev', url: 'https://github.com/AnasAnsar1/spring-petclinic.git'
            }
        }
        stage('build & Analysis') {
            steps {
                withSonarQubeEnv('SONAR_DEFAULT') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }
}