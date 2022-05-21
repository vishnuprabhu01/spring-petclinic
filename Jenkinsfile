pipeline{
    agent {label 'mvn_new1'}
    stages{
        stage('clone the git repo'){
            steps{
                git branch: 'main', url: 'https://github.com/vishnuprabhu01/spring-petclinic.git'
            }
        }
        stage('build the code') {
            steps{
                sh 'mvn clean package'
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

