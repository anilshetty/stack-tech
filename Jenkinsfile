pipeline {
    agent any

    tools {
        maven 'apache-maven-3.0.1'
        
    }

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build & Deploy package') {
          steps{
            script {
              def server = Artifactory.server('local-server')
              def rtMaven = Artifactory.newMavenBuild()
              rtMaven.resolver server: server, releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot'
              rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'
              rtMaven.tool = 'Maven 3.3.9'
              def buildInfo = rtMaven.run pom: 'pom.xml', goals: 'install'
              server.publishBuildInfo buildInfo
            }
          }
        }

        stage ('SonarQube Analysis') {
          steps{
              
              sh 'echo sonaring'
            
          }

          post {
              success {
                  archiveArtifacts 'target/*.jar'
              }
          }
        }

        stage ('Deploy to EC2') {
          steps {
            wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {
              ansiblePlaybook(
                playbook: 'playbook1.yml',
                colorized: true)
            }
          }
        }

    }
}
