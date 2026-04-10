@Library("Shared") _

pipeline {
    agent {
        label 'ubuntu'
    }

    environment {
        IMAGE_NAME = 'notes-app'
    }

    stages {
        stage('Hello') {
            steps {
                script {
                    hello()
                }
            }
        }

        stage('Code') {
            steps {
                script {
                    clone("main", "https://github.com/SumnRanjan/jenkins-django-notes-app.git")
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    buildImage(env.IMAGE_NAME)
                }
            }
        }

        stage('Push To DockerHub') {
            steps {
                script {
                    pushToDockerHub(env.IMAGE_NAME, 'dockerHubCred')
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    runTests()
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    deployApp()
                }
            }
        }
    }
}
