pipeline {
    agent any // Specifies that the pipeline can run on any available agent
    
    stages {
        stage("Clone Code") {
            steps {
                echo "Cloning the code" // Simulating code repository cloning
                git url:"https://github.com/krishna078/django-notes-app.git", branch: "main"
            }
        }
        
        stage("Build Image") {
            steps {
                echo "Building the Docker image" // Simulating image building
                sh "docker build -t my-note-app ."
            }
        }
        
        stage("Push to Docker Hub") {
            steps {
                echo "Pushing the image to Docker Hub" // Simulating image push
                // Using withCredentials to securely access Docker Hub credentials
                    withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubpass')]) {
                        sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest "
                        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubpass} "
                        sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                    }
            }          
        }
        
        stage("Deploy Container") {
            steps {
                echo "Deploying the Docker container" // Simulating container deployment
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
