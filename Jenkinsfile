pipeline {
    agent any

    environment {
        REGISTRY = "ec2-51-20-122-193.eu-north-1.compute.amazonaws.com"
        PROJECT  = "orix-citest"
        IMAGE    = "web01"
        TAG      = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                script {
                    app = docker.build("${REGISTRY}/${PROJECT}/${IMAGE}")
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry("https://${REGISTRY}", "harbor-reg") {
                        app.push(TAG)
                        app.push("latest")
                    }
                }
            }
        }
    }
}

