pipeline {
  agent env
  stagets {
    staget('git_scm_update') {
      steps{
        git url: "https://github.com/thedeny1106/ktcloudinfra4jenkins.git", branch: "main"
      }
    }
    stage('delivery and deployment using k8s') {
      steps {
        sh '''
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf get no"
        '''
      }
    }
  }
}
