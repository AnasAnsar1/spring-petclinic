pipeline {
    agent { label 'JDK-MVN1'}
        stages{
            stage('git'){
                steps{
                    git url: 'https://github.com/AnasAnsar1/spring-petclinic.git' , branch: 'ver_1.0'
                }
            }
            stage('build'){
                steps{
                    sh 'mvn package'
                    junit '**/surefire-reports/*.xml'
                }
            }
        }
}