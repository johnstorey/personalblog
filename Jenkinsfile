pipeline {
  agent { 
    docker {
      image 'jojomi/hugo'
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
          sh 'mkdir -p themes && cd themes && git clone https://github.com/budparr/gohugo-theme-ananke.git && cd ..'
          sh 'git submodule init'
          sh 'cd themes/ananke; ls -la; cd ..'
          sh "ssh -o StrictHostKeyChecking=no root@blog.johnstorey.org 'rm -rf /var/www/html/*' " 
          sh 'scp -r public/* root@blog.johnstorey.org:/var/www/html '
        }
      }
    }
  }
}

