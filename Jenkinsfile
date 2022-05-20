pipeline{
    agent {label 'mvn3.0.5'}
    stages{
        stage('clone the git repo'){
            steps{
                git branch: 'main', url: 'https://github.com/vishnuprabhu01/spring-petclinic.git'
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

https://github.com/vishnuprabhu01/spring-petclinic.git