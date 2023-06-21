pipeline {
    agent any
    environment {
        dockerimagename = "bigjack213/flask-k8s-test"
        dockerImage = ""
        PROJECT_ID = 'flask-k8s-test-390411'
        CLUSTER_NAME = 'autopilot-cluster-1'
        LOCATION = 'europe-central2'
        CREDENTIALS_ID = 'flask-k8s-test'
    }

    stages {
        stage ('Checkout source') {
            steps {
                git credentialsId: 'github-credentials', url: 'https://github.com/JanKaczmarski/flask-k8s-test.git'
            }
        }

        stage ('Build image') {
            steps{
                script {
                    dockerImage = docker.build(dockerimagename)
                }
            }
        }

        stage ('Push image to docker-hub') {
            steps {
                script{
                    withDockerRegistry([ credentialsId: "dockerhub-credentials", url: ""]) {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
