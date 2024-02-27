
pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_CREDENTIALS = 'docker-hub-repo'
        IMAGE_NAME = 'sunbestamb/nodejs:1.0'
    }

    stages {
        stage('Increment Version') {
            steps {
                script {
                    def incrementedVersion = incrementVersion()
                    env.APP_VERSION = incrementedVersion
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    runTests()
                }
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                script {
                    buildAndPushDockerImage(env.APP_VERSION, IMAGE_NAME, DOCKER_REGISTRY, DOCKER_CREDENTIALS)
                }
            }
        }
        stage('Commit to Git') {
            steps {
                script {
                    commitToGit()
                }
            }
        }
    }
}
