pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "your-dockerhub-username/node-app"
    }

    stages {
        stage("Clone Repository") {
            steps {
                git "https://github.com/yourusername/my-cicd-app.git"
            }
        }

        stage("Build Docker Image") {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage("Push Docker Image") {
            steps {
                script {
                    docker.withRegistry("https://index.docker.io/v1/", "dockerhub-credentials-id") {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage("Deploy to Kubernetes") {
            steps {
                withKubeConfig([credentialsId: "kubeconfig-credentials-id"]) {
                    sh "kubectl apply -f k8s-deployment.yaml"
                }
            }
        }
    }
}
