node('OPENJDK-11-MVN') {
    stage('vcs') {
        git branch: 'main', url: 'https://github.com/sudhakarpolavarapu/spring-petclinic.git'
    }
    stage("build") {
        sh 'mvn package'
    }
    stage("archive results") {
        junit '**/surefire-reports/*.xml'