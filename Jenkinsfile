pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        git(url: 'https://github.com/dinesh99088/offers', branch: 'master', changelog: true, poll: true)
      }
    }

  }
}