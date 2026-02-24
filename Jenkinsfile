pipeline {
    agent any
    environment { 
      DOCKER_USER = "sagartikare935335" 
    }
    stages {

        stage('get code') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/sagartikare/crud-dd-task-mean-app.git'
            }
        }

        stage('build backend image') {
            steps {
                sh 'docker build -t DOCKER_USER/mean-backend ./backend'
            }
        }

        stage('build frontend image') {
            steps {
                sh 'docker build -t DOCKER_USER/mean-frontend ./frontend'
            }
        }

        stage('docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('push images') {
            steps {
                sh 'docker push DOCKER_USER/mean-backend'
                sh 'docker push DOCKER_USER/mean-frontend'
            }
        }

        stage('deploy') {
            steps {
                sh '''
                cd /home/ec2-user/crud-dd-task-mean-app || true

                if [ ! -d ".git" ]; then
                    git clone https://github.com/sagartikare/crud-dd-task-mean-app.git
                    cd crud-dd-task-mean-app
                fi

                git pull
                docker compose down
                docker compose up -d
                '''
            }
        }
    }
}
