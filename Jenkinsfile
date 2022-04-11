node('jenkins_agent_ansible'){
    stage('build'){
        sh 'date'
    }
    stage('start_unit_test'){
        sh 'pip install -e '.[test]''
    }  
}
