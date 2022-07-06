pipeline {
  agent {
    node {
      label 'centos7'
    }

  }
  stages {
    stage('checkout code') {
      parallel {
        stage('checkout code') {
          steps {
            git(credentialsId: 'github', url: 'git@github.com:nananoam123/NodeJS-EmptySiteTemplate.git', branch: 'master')
          }
        }

        stage('say hello to me ') {
          steps {
            sh 'echo "hello"'
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test App') {
      parallel {
        stage('Run the App') {
          steps {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              sh 'node server.js'
            }

          }
        }

        stage('check if app is running') {
          steps {
            sh '''sleep 5
curl localhost:8081 
if [ $(echo $?) -eq 0 ]; 
then
  echo "success" 
  ps -ef | grep node | awk \'{print $2}\' | head -n 1 | xargs kill
  exit 0
else 
  echo "failure"
  exit 1
fi  '''
          }
        }

      }
    }

    stage('Package') {
      steps {
        sh '''mkdir target && rsync -Rr . target/
tar -czvf package-$BUILD_ID.tar.gz target/
'''
      }
    }

    stage('Archive Artifact') {
      steps {
        archiveArtifacts '*.tar.gz'
        sh 'rm -rf *'
      }
    }

  }
}