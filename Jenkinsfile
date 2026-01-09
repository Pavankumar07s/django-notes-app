@Library("Shared") _
pipeline {
    agent { label "pavan" }

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
                    clone("https://github.com/Pavankumar07s/django-notes-app.git", "main")
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    docker_build("notes-app", "latest", "pavankumar07s")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker_push("notes-app", "latest", "pavankumar07s")
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker compose down || true
                docker compose up -d --build
                '''
            }
        }
    }
}
