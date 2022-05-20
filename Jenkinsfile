pipeline{
    agent {label 'JDK11'}
    stages{
        stage('clone the git repo'){
            steps{
                git "https://github.com/vishnuprabhu01/spring-petclinic.git"
            }
        }
        stage('build the code') {
            steps{
                sh 'mvn package'
            }
        }
        stage('run the junit test'){
            steps{
                junit '**/*/*.xml'
            }
        }
        stage('Archive the artifacts'){
            steps{
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            }
        }

    }

}