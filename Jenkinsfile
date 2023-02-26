pipeline{
    agent any
    parameters{
        choice(name:'BRANCH_TO_BUILD', choices: ['main', 'REL_INT_1.0'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')
        
    }

    stages{
        stage('vcs'){
            steps {
                git branch: "${params.BRANCH_TO_BUILD}",
                    url: 'https://github.com/sashi3333/spring-petclinic.git'
            }
        }
        stage('build'){
            steps{
                sh "/opt/apache-maven-3.9.0/bin/mvn $(params.MAVEN_GOAL)"
            }
        }
        stage('archive results'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}