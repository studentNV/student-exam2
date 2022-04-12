pipeline {
    agent { label 'linux' }
    environment{
        DOCKERHUB_CREDENTIALS = credentials('studentnv-dockerhub')
    }
    stages {
        stage('pull_rep') {
            steps {
                sh '''
                cd /opt/student-exam2
                git pull origin master
                '''
            }
        }
        stage('start_unit_test') {
            steps {
                sh '''
                cd /opt/student-exam2
                . venv/bin/activate
                pip install -e '.[test]'
                coverage run -m pytest
                coverage report
                '''
            }
        }
        stage('build_docker_app') {
            steps {
                sh '''
                cd /opt/student-exam2
                    sudo docker build -t exam2:web_app .
                '''
            }
        }
        stage('app') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push_docker_hub') {
            steps {
                sh 'sudo docker push studentnv/exam2:web_app'
            }
        }
    }
    
}
