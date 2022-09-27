node('OPENJDK-11-MVN') {
    stage('vcs') {
        git branch: 'main', url: 'https://github.com/sudhakarpolavarapu/spring-petclinic.git'
    }
    stage("build") {
        sh '/opt/apache-maven-3.6.3/bin/mvn package'
    }
    stage("archive results") {
        junit '**/surefire-reports/*.xml'