pipeline{
    agent {label 'mvn_new1'}
    triggers {  pollSCM '*/30 * * * *'}
    parameters {  string defaultValue: 'package', description: 'select the goal', name: 'goal'}
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

