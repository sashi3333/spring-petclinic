pipeline{
    agent any
    stages{
        stage('vcs'){
            steps {
                git branch: 'REL_INT_1.0',
                url: 'https://github.com/sashi3333/spring-petclinic.git'
            }
        }
        stage('build'){
            steps{
                sh '/usr/share/maven/bin/mvn package'
            }
        }
        stage('archive results'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}