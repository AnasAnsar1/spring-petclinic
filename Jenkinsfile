pipeline{
    agent { label 'JDK11_MVN'}
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
                junit '**/surefire-reports/*.xml'   
            }
        }
    }
    post {
            always {
                mail subject: "Build started",
                     body: "Build is started on node $env.NODE_NAME",
                     to: "anasansarii78@gmail.com"
            }
            failure {
                mail subject: "Build Failed",
                     body: "Build failed on node $env.NODE_NAME",
                     to: "anasansarii78@gmail.com"
            }
            success {
                mail subject: "Build Success",
                     body: "Build Success on node $env.NODE_NAME",
                     to: "anasansarii78@gmail.com"
            }
        }
}