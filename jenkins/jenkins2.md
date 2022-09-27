pipeline {
    agent  { label 'OPENJDK-11-MVN' }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['master', 'main'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')

    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/sudhakarpolavarapu/spring-petclinic.git'
            }
            
        }
        stage('build') {
            steps {
                sh "mvn packag ${params.MAVEN_GOAL}"
            }
        }
        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}