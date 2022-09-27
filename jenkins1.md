pipeline {
    agent  { label 'OPENJDK-11-MVN' }
    stages {
        stage('vcs') {
            steps {
                git branch: 'REL_INT_1.0', url: 'https://github.com/sudhakarpolavarapu/spring-petclinic.git'
            }

        }
        stage('build') {
            steps {
                sh '/opt/apache-maven-3.8.6/bin/mvn package'
            }
        }
        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
    }

}