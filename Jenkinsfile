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

        stage('Deploy to Kubernetes') {
            steps {
                bat '"%KUBECTL%" apply --validate=false -f deployment.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '"%KUBECTL%" rollout status deployment/cicd-web-app --timeout=120s'
                bat '"%KUBECTL%" get deployments'
                bat '"%KUBECTL%" get pods'
            }
        }
    }
}
