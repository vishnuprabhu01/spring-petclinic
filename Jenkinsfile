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
                withSonarQubeEnv('SONAR_MAIN') {
               sh 'mvn clean package sonar:sonar'
                           }
            }             
        }
          stage('Artifactory-Configuration') {
            steps {
                rtMavenDeployer (
                    id: 'spc-deployer',
                    serverId: 'JROG_NEW',
                    releaseRepo: 'springpetclinic-libs-release-local',
                    snapshotRepo: 'springpetcinic-libs-snapshot-local',

                )
            }
        }
        stage('Build the Code and sonarqube-analysis') {
            steps {

                rtMavenRun (
                    // Tool name from Jenkins configuration.
                    tool: 'mvn_new1',
                    pom: 'pom.xml',
                    goals: 'clean install',
                    // Maven options.
                    deployerId: 'spc-deployer',
                )

            }
        }
        stage('quality gate'){
            steps{
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
            }
        }
        }       
    }
}

