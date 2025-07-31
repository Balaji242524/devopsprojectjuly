pipeline {
    agent any

    environment {
        docker_image = 'balaji2404/devopsprojectjuly:v1'
    }

    stages {
        stage("Check-out") {
            steps {
                git branch: 'main', url: 'https://github.com/Balaji242524/devopsprojectjuly'
            }
        }

        stage("Build image") {
            steps {
                sh '''
                    echo "Building Docker image"
                    docker build -t $docker_image .
                '''
            }
        }

        stage("Push Docker image") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "Logging in to DockerHub..."
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin

                        echo "Pushing Docker image..."
                        docker push $docker_image
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}
