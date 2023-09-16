pipeline {
  agent { label 'GOL' }

  triggers { pollSCM ('* * * * *') }

  stages {
    stage('SCM') {
      steps {
        git branch: 'qa', url: 'https://github.com/AnasAnsar1/spring-petclinic.git'
      }
    }

    stage('set_deployer') {
      steps {
        rtMavenDeployer (
        id: 'JFROG_ARTI',
        serverId: 'JFROG_ARTI',
        releaseRepo: 'jenkins-integration',
        snapshotRepo: 'jenkins-integration',
      )
      }
    }

    stage('mvn_build & deploy_artifact') {
      steps {
        rtMavenRun (
          tool: 'Maven 3.6.3', 
          pom: 'pom.xml',
          goals: 'clean install',
          deployerId: 'JFROG_ARTI',
      )
      }
    }

  }
}

