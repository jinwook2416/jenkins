pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/beomtaek78/ktcloudinfrajenkins.git', branch: 'main'
      }
    }
    stage('build docker image') {
      steps {
        sh '''
        docker build -t dlwlsdnr24/ktcloudinfra4:0727 .
        docker bush dlwlsdnr24/ktcloudinfra4:0727
        '''
      }
    }
    stage('delivery and deployment using k8s') {
      steps {
        sh '''
        ansible master -m copy -a "src=deploy.yml dest=/root/deploy.yml"
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf get no"
        '''
      }
    }
  }
  post {
    success {
      echo 'success'
    }
    failure {
      echo 'failure'
    }
  }
}
