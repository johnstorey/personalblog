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
        sh 'cp /root/ssh/personal-blog* /root/.ssh'
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

