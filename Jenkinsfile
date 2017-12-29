pipeline {
  agent { docker {
          image 'jojomi/hugo'
	  args '-v /home/johnstorey/.ssh:/root/ssh'
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
        sshagent(['personal-blog']) {
          sh 'echo SSH_AUTH_SOCK=$SSH_AUTH_SOCK'
          sh 'ls -al $SSH_AUTH_SOCK || true'
          sh 'ls -la'
          sh "ssh -o StrictHostKeyChecking=no root@blog.johnstorey.org 'rm -rf /var/www/html/*' " 
          sh 'scp -r public/* root@blog.johnstorey.org:/var/www/html '
        }
      }
    }
  }
}

