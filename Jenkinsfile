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
        sh' sudo docker build -t balasubramaniyand/kill:latest /var/lib/jenkins/workspace/kill'
        sh 'sudo docker tag  balasubramaniyand/kill:latest balasubramaniyand/love:${BUILD_NUMBER}'
    }
    }
    stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push balasubramaniyand/kill:latest'
                sh 'sudo docker image push balasubramaniyand/kill:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/kil/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}


