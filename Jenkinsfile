pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig01')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/kitsanaphon1/k8s-Webapi-01.git', branch: 'dev01'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "[INFO] Deploying manifests..."
                    kubectl version --client
                    kubectl apply -f k8s-api.yaml
                    kubectl apply -f k8s-app.yaml
                    kubectl apply -f k8s-postgres.yaml
                '''
            }
        }
    }
}
