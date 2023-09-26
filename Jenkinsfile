pipeline {
    agent any
    stages {
        stage ( 'Pull Code From Github'){
        steps{
           git 'https://github.com/balasubramaniyand/07k8sprojcet.git'
        }
    }
    stage('docker'){
    steps {
        sh'sudo docker images'
    }
}
stage('Build the Dcoker images'){
    steps{
        sh' sudo docker build -t balasubramaniyand/love01:latest /var/lib/jenkins/workspace/love'
        sh 'sudo docker tag  balasubramaniyand/love01:latest balasubramaniyand/love:${BUILD_NUMBER}'
    }
    }
    stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push balasubramaniyand/love01:latest'
                sh 'sudo docker image push balasubramaniyand/love01:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/love/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}


