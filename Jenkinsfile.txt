pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    http://docker.build("my-java-app:${env.BUILD_ID}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run tests if needed
                    // For a basic Java program, you might not need this stage
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy the Docker image as needed
                    // This could be pushing to a Docker registry or deploying to a Kubernetes cluster
                }
            }
        }
    }

    post {
        success {
            // Do something on successful build
            echo 'Build successful!'

            // Clean up Docker images after successful build (optional)
            cleanWs()
            docker.image("my-java-app:${env.BUILD_ID}").remove()
        }
        failure {
            // Do something on build failure
            echo 'Build failed!'
        }
    }
}
 