pipeline {
    agent {
        docker {
            image 'bitnami/kubectl:latest' // ใช้ Docker image ที่มี kubectl พร้อมใช้งาน
            args '-v $HOME/.kube:/root/.kube' // ถ้าต้องใช้ .kube (อาจข้ามได้ถ้าใช้ KUBECONFIG)
        }
    }

    environment {
        KUBECONFIG = credentials('kubeconfig01') // ใช้ Secret file จาก Jenkins Credentials
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
                    kubectl version --client
                    kubectl apply -f k8s-api.yaml
                    kubectl apply -f k8s-app.yaml
                    kubectl apply -f k8s-postgres.yaml
                '''
            }
        }
    }
}
