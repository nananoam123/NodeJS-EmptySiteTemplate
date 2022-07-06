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

    stage('test') {
      parallel {
        stage('run app') {
          steps {
            sh 'node server.js'
          }
        }

        stage('test app') {
          steps {
            sh '''curl localhost:8081
if [[ $(echo $?) == 0 ]] then 
   echo "success"
   ps -ef | grep node | awk {"print $2"}
   exit 0
else 

 echo "fail"
 exit 1'''
          }
        }

      }
    }

  }
}
