pipeline {
    agent any

    environment {
        RELEASE_NAME = "employee-app"
        CHART_PATH = "."
        NAMESPACE = "default"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/YOUR_GITHUB_USERNAME/employee-management-helm.git'
            }
        }

        stage('Helm Version') {
            steps {
                bat 'helm version'
            }
        }

        stage('Helm Lint') {
            steps {
                bat 'helm lint %CHART_PATH%'
            }
        }

        stage('Helm Upgrade') {
            steps {
                bat '''
                helm upgrade --install %RELEASE_NAME% %CHART_PATH% ^
                --namespace %NAMESPACE%
                '''
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
            echo '✅ Helm deployment completed successfully.'
        }

        failure {
            echo '❌ Helm deployment failed.'
        }
    }
}