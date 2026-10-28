
pipeline {
    agent any

    environment {
        bat '"%DOCKER%" build -t jenkins-k8s-lab:latest .'
        KUBECONFIG = 'C:\\Users\\POOVARASAN\\.kube\\config'
        IMAGE = 'jenkins-k8s-lab:latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE% .'
            }
        }

        stage('Load Image into Kubernetes') {
            steps {
                bat 'kind load docker-image %IMAGE% --name docker-desktop'
            }
        }

        stage('Deploy Application') {
            steps {
                bat '"%KUBECTL%" apply -f deployment.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '"%KUBECTL%" rollout status deployment/cicd-web-app --timeout=180s'
                bat '"%KUBECTL%" get pods -l app=cicd-web-app'
            }
        }
    }
}
