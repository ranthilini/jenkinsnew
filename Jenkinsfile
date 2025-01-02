pipeline {
    agent any

    stages {
       stage('Clone Repository') {
    steps {
        git branch: 'main', url: 'https://github.com/ranthilini/jenkinsnew.git'
          }
      }


        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    def app = docker.build("communication_backend:latest")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Stop any running container and remove it
                script {
                    try {
                        sh "docker stop website_container"
                        sh "docker rm website_container"
                    } catch (Exception e) {
                        echo "No container to stop"
                    }
                    // Run the new Docker container
                    sh "docker run -d --name website_container -p 8089:80 my_website4:latest"
                }
            }
        }
    }

    post {
        always {
            // Clean up unused images
            sh "docker system prune -f"
        }
    }
}

