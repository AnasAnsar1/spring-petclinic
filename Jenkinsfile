pipeline{
    agent {label 'JDK11_MVN'}
    stages{
        stage('vcs'){
            steps{
                mail subject: "Build is starting",
                     body: "Build is cloned and starting on node $env.NODE_NAME",
                     to: "anasansarii78@gmail.com"
                    git url: "https://github.com/AnasAnsar1/spring-petclinic.git", branch: "ver_1.0"
            }
        }
        stage('artifactory_config'){
            steps{
                rtMavenDeployer (
                id: 'MAVEN_DEPLOYER',
                serverId: 'JFROG_DEFAULT',
                releaseRepo: 'mv-libs-release-local',
                snapshotRepo: 'mv-libs-snapshot-local'
                )
            }
        }
        stage('Build && analysis'){
            steps{
                withSonarQubeEnv('SONAR_DEFAULT'){
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage('Maven_run'){
            steps{
                rtMavenRun (
                tool: 'MAVEN_DEFAULT',
                pom: 'pom.xml',
                goals: 'clean install',
                deployerId: "MAVEN_DEFAULT"
           )
                 }
        }
    }
    post{
        always{
            mail subject:"Build is finished",
                 body: "Build is done",
                 to: "anasansarii78@gmail.com"
        }
        failure{
            mail subject:"Build is failed",
                 body: "Build has failed please try to fix it ASAP",
                 to: "anasansarii78@gmail.com"
        }
        success{
            mail subject:"Build is success",
                 body: "Build has succeeded",
                 to: "anasansarii78@gmail.com"
        }
    }
}