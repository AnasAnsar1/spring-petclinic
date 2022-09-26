node('JDK-MVN1') {
    stage('git') {
    git branch: 'ver_1.0', url: 'https://github.com/AnasAnsar1/spring-petclinic.git'
}
stage('build') {
    sh 'mvn package'
}
stage('Archive') {
    junit '**/surefire-reports/*.xml'
}
}