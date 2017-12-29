pipeline {
  agent { docker {
          image 'jojomi/hugo'
	  args '-p 1337:1337'
          }
        }
  stages {
    stage('build') {
      steps {
        sh 'hugo'
      }
    }
    stage('deploy') {
      sh 'echo deploy securely with ssh'
    }
  }
}

