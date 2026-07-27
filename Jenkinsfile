pipeline {
    agent any
    stages {
        stage('Git SCM Update') {
            steps {
                git url: 'https://github.com/thedeny1106/ktcloudinfra4jenkins.git',branch: 'main'
            }
        }
        stage('Build & Push Docker Image') {
            steps {
                sh '''
                docker build -t thedeny1106/ktcloudinfra4:0727 .
                docker push thedeny1106/ktcloudinfra4:0727
                '''
            }
        }
        stage('Copy deploy.yml to Master') {
            steps {
                sh '''
                ansible master -m copy -a "src=deploy.yml dest=/root/deploy.yml"
                '''
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf apply -f /root/deploy.yml"
                '''
            }
        }
    }
}
