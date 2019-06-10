pipeline {
  agent any
  stages {
    stage('checkout') {
      parallel {
        stage('checkout') {
          steps {
            git(url: 'https://github.com/Egon2018/order.git', branch: 'master', changelog: true)
          }
        }
        stage('') {
          steps {
            sh 'sh \'pwd\''
          }
        }
      }
    }
    stage('sleep') {
      steps {
        sleep 30
      }
    }
    stage('bulid') {
      steps {
        build 'order'
      }
    }
  }
  environment {
    branch = 'master'
    code = 'github'
  }
}