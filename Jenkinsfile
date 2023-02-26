pipeline{
    agent any
    parameters{
        choice(name:'BRANCH_TO_BUILD', choices: ['main', 'REL_INT_1.0'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')
        
    }
    triggers{

        pollscm('* * * * *')
        
    }
    stages{
        stage('vcs'){
            steps {
                mail subject: 'Build Started', 
                    body: 'Build started',
                    to: 'sashidhar3333@mail.com'
                git branch: "${params.BRANCH_TO_BUILD}",
                    url: 'https://github.com/sashi3333/spring-petclinic.git'
            }
        }
        stage('build'){
            steps{
                sh "/opt/apache-maven-3.9.0/bin/mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('archive results'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
    }

    post {
        always{
            echo 'Job completed'
        }
        failure{
            mail subject: 'Build Failure', 
                 body: 'Build failed',
                 to: 'sashidhar3333@mail.com'
        }
        success{
            junit '**/surefire-reports/*.xml'
        }
    }
}