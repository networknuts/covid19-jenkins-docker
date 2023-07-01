pipeline {
    agent any

    stages {
        stage('Go to Git') {
            steps {
                // This stage is to checkout the Git Repo
                checkout scm
            }
        }
        stage('Build and Push') {
            steps {
                script {
                    // Defining Docker Image and Tag variables
                    def dockerImage = "aryansr/jenkins-covid-app"
                    def dockerTag = "v3"
                    def dockerCredentialsId = "aryan-docker"
                    // Starting the Build Process
                    def dockerBuild = docker.build("${dockerImage}:${dockerTag}",'.')
                    docker.withRegistry('', dockerCredentialsId) {
                        dockerBuild.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                        sh 'docker run -d -p 8000:8000 ${dockerImage}:${dockerTag}'
            }
        }
    }
}
}
