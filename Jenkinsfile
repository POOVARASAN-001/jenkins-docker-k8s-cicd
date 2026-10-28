
pipeline {
    agent any

    environment {
        DOCKER = 'D:\\DockerApp\\resources\\bin\\docker.exe'
        KUBECTL = 'D:\\DockerApp\\resources\\bin\\kubectl.exe'
        KUBECONFIG = 'C:\\Users\\POOVARASAN\\.kube\\config'
        IMAGE = 'jenkins-k8s-lab:latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                bat '"%DOCKER%" build -t %IMAGE% .'
            }
        }

        
        stage('Load Image into Kubernetes') {
            steps {
                bat '"%DOCKER%" images'
            }
        }


        stage('Deploy Application') {
            steps {
                bat '"%KUBECTL%" apply -f deployment.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '"%KUBECTL%" rollout status deployment/jenkins-k8s-lab --timeout=120s'
                bat '"%KUBECTL%" get pods'
                bat '"%KUBECTL%" get services'
            }
        }
    }
}
