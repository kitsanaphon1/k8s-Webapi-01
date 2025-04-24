pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig01') // ดึง kubeconfig จาก Jenkins credentials
    }

    stages {
        stage('Checkout Source') {
            steps {
                git url: 'https://github.com/kitsanaphon1/k8s-Webapi-01.git', branch: 'dev01'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    echo "[INFO] Deploying k8s manifests..."
                    kubectl apply -f k8s-api.yaml
                    kubectl apply -f k8s-app.yaml
                    kubectl apply -f k8s-postgres.yaml
                '''
            }
        }
    }
}
