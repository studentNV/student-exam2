node('jenkins_agent'){
    stage('start_unit_test'){
        sh '''cd /opt/student-exam2
        . venv/bin/activate
        pip install -e '.[test]'
        coverage run -m pytest
        coverage report
        '''
    }
    stage('start_unit_test'){
        def image = docker.build("web")
    }
}
