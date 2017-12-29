pipeline {
  agent { docker {
          'jojomi/hugo'
	  args '-p 1337:1337'
          }
        }
  stages {
    stage('build') {
      steps {
        sh 'echo building'
      }
    }
  }
}

