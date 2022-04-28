pipeline {
    agent { label 'linux' }
    environment{
        DOCKERHUB_CREDENTIALS = credentials('studentnv-dockerhub')
    }
    stages {
        stage('pull_rep') {
            steps {
                echo '> Github pull web app repository.'
                sh ' cd /opt/student-exam2 && git pull origin master '
            }
        }
        stage('start_unit_tests') {
            steps {
                echo '> Start unit tests.'
                sh '''
                cd /opt/student-exam2
                . venv/bin/activate
                coverage run -m pytest
                coverage report
                '''
            }
        }
        stage('build_docker_app') {
            steps {
                echo '> Build docker web app.'
                sh ' cd /opt/student-exam2 && sudo docker build -t exam2:web_app . '
            }
        }
        stage('login_dockerhub') {
            steps {
                echo '> Login docker hub.'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push_docker_hub') {
            steps {
                echo '> Push docker hub.'
                sh 'sudo docker push studentnv/exam2:web_app'
            }
        }
    }
}

