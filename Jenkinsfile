pipeline {
    agent none
    
    triggers {
        pollSCM('* * * * *')
    }
    
    stages {
        stage('Build') {
            agent { 
                node {
                    label 'docker-agent-python'
                }
            }
            steps {
                script {
                    echo "Building.."
                    sh '''
                    cd myapp
                    pip install -r requirements.txt
                    '''
                }
            }
        }
        
        stage('Test') {
            agent { 
                node {
                    label 'docker-agent-python'
                }
            }
            steps {
                script {
                    echo "Testing.."
                    sh '''
                    cd myapp
                    python3 hello.py
                    python3 hello.py --name=Brad
                    '''
                }
            }
        }
        
        stage('Deliver') {
            agent { 
                node {
                    label 'docker-agent-python'
                }
            }
            steps {
                script {
                    echo 'Deliver....'
                    sh '''
                    echo "doing delivery stuff.."
                    '''
                }
            }
        }
    }
}
