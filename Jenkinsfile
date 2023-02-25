pipeline{
    agent any
    parameters{
        choice(name:'BRANCH_TO_BUILD', choices: ['main','REL_INT_1.0'] description: 'Branch to build')
        string(name:'MAVEN_GOAL', defaultValue: 'package', description: 'Maven goals')
    }

    stages{
        stage('vcs'){
            steps {
                git branch: '${params.BRANCH_TO_BUILD}',
                url: 'https://github.com/sashi3333/spring-petclinic.git'
            }
        }
        stage('build'){
            steps{
                sh '/usr/share/maven/bin/mvn ${params.MAVEN_GOAL}'
            }
        }
        stage('archive results'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}