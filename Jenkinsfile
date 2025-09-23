@Library("shared") _
pipeline {
    agent {label "praveen" }
    stages{
        stage('Code Clone') {
            steps {
                script{
                    clone("https://github.com/Praveen-cloud-dev/django-notes-app.git","dev")
                }
            }
        }
        stage('build') {
            steps {
                script{
                    docker_build("notes-app","latest","cloudhere2")
                }
            }
        }
        stage('push image') {
            steps {
                script{
                    docker_push("notes-app","latest","cloudhere2")
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'this is deploying the code'
                sh "docker compose down && docker compose up -d"
                echo "deployment sucess! using scm"
            }
        }
    }
}
