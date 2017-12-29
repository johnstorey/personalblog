pipeline {
  agent { docker {
          image 'jojomi/hugo'
	  args '-p 1337:1337'
          }
        }
  stages {
    stage('Replace With Custom Image') {
      steps {
        sh 'apk add --update openssh'
      }
    }
    stage('Build') {
      steps {
        sh 'hugo'
      }
    }
    stage('Deploy') {
      steps {
        sh "ssh -i ~/.ssh/personal-blog root@blog.johnstorey.org 'rm -rf /var/www/html/*' " 
        sh 'scp -r -i ~/.ssh/personal-blog public/* root@blog.johnstorey.org:/var/www/html '
      }
    }
  }
}

