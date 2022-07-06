pipeline {
  agent any
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

  }
}