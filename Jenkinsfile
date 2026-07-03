pipeline {
    agent any

    environment {
        RELEASE_NAME = "employee-app"
        NAMESPACE = "default"
        CHART_PATH = "."
        KUBECONFIG = "C:\\Users\\saifa\\.kube\\config"
    }

    stages {

        stage('Helm Version') {
            steps {
                bat 'helm version'
            }
        }

        stage('Kubectl Version') {
            steps {
                bat 'kubectl version --client'
            }
        }

        stage('Check Kubernetes') {
            steps {
                bat 'kubectl config current-context'
                bat 'kubectl get nodes'
            }
        }

        stage('Helm Lint') {
            steps {
                bat 'helm lint %CHART_PATH%'
            }
        }

        stage('Helm Upgrade') {
            steps {
                bat 'helm upgrade --install %RELEASE_NAME% %CHART_PATH% --namespace %NAMESPACE%'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get svc'
                bat 'kubectl get ingress'
            }
        }
    }

    post {
        success {
            echo 'Helm deployment completed successfully.'
        }

        failure {
            echo 'Helm deployment failed.'
        }

        always {
            cleanWs()
        }
    }
}