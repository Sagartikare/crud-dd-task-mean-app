pipeline {
    agent any

    environment {
        DOCKER_USER = "sagartikare935335"
        APP_DIR = "/var/lib/jenkins/app/crud-dd-task-mean-app"
    }

    stages {

        stage('build backend image') {
            steps {
                sh 'docker build -t $DOCKER_USER/mean-backend ./backend'
            }
        }

        stage('build frontend image') {
            steps {
                sh 'docker build -t $DOCKER_USER/mean-frontend ./frontend'
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
                sh 'docker push $DOCKER_USER/mean-backend'
                sh 'docker push $DOCKER_USER/mean-frontend'
            }
        }

        stage('deploy') {
            steps {
                sh '''
                if [ ! -d "$APP_DIR" ]; then
                    git clone https://github.com/sagartikare/crud-dd-task-mean-app.git $APP_DIR
                fi

                cd $APP_DIR
                git pull
                docker-compose down
		docker-compose up -d
                '''
       
            }
        }
    }
}
