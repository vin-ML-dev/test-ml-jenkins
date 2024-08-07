pipeline {
    agent {
        docker {
            image 'python:3.9.18-slim'
        }
    }
    stages {
        stage('Create and Activate Virtual Environment') {
            steps {
                script {
                    sh '''
                        python3 -m venv myenv
                        . myenv/bin/activate
                        pip install -r requirements.txt
                        
                    '''
                }
            }
        }
        
        stage('train model') {
            steps {
                script {
                    sh '''
                       
                        . myenv/bin/activate
                        python train.py
                        
                    '''
                }
            }
        }
        
        stage('test') {
            steps {
                script {
                    sh '''
                       
                        . myenv/bin/activate
                        python test.py
                        
                    '''
                }
            }
        }
    }
}

