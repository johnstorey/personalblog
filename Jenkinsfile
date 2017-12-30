pipeline {
  agent { 
    docker {
      image 'jojomi/hugo'
    }
  }
  stages {
    stage('Replace With Custom Image') {
      steps {
        sh 'apk add --update openssh git'
      }
    }
    stage('Build') {
      steps {
        sh 'mkdir -p themes'
        sh 'rm -rf themes/*'
	sh 'git clone https://github.com/budparr/gohugo-theme-ananke.git themes/gohugo-theme-ananke'
        sh 'hugo' 
      }
    }
    stage('Deploy') {
      steps {
        sshagent(['personal-blog']) {
          sh 'echo SSH_AUTH_SOCK=$SSH_AUTH_SOCK'
          sh 'ls -al $SSH_AUTH_SOCK || true'
          sh "ssh -o StrictHostKeyChecking=no root@blog.johnstorey.org 'rm -rf /var/www/html/*' " 
          sh 'scp -r public/* root@blog.johnstorey.org:/var/www/html '
        }
      }
    }
  }
}

