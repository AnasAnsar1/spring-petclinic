pipeline{
    agent { label 'JDK-MVN1'}
    parameters { choice(name: 'branch', choices: ['main', 'ver_1.0'], description: 'chose a branch')
                 string(name: 'goals', defaultValue: 'mvn', description: 'Put in goals for maven')}
    stages{
        stage('vcs'){
            steps{
            git url: 'https://github.com/AnasAnsar1/spring-petclinic.git', branch: "${params.branch}"
            }
        }
        stage('build'){
            steps{
                sh "${params.goals}"
            }
        }
    }
}