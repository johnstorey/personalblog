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
        sh 'mkdir -p /root/.ssh'
        sh 'ls -la /root'
        sh 'ls -la /root/ssh/*'
        sh 'cp /root/ssh/personal-blog /root/.ssh'
        sh 'cp /root/ssh/personal-blog.pub /root/.ssh'
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
          sh "ssh root@blog.johnstorey.org 'rm -rf /var/www/html/*' " 
          sh 'scp -r public/* root@blog.johnstorey.org:/var/www/html '
        }
      }
    }
  }
}

