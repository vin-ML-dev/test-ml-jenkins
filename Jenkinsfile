pipeline {
    agent {
        docker {
            image 'python:3.9.18-slim'
        }
    }
    
    environment {
         CONTAINER_NAME = "run-iris-model"
         CONTAINER_NAME_DEPLOY = "deploy-iris-model"
         DOCKER_IMAGE = 'flask-iris-mlops'
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
        stage('Deploy') {
              steps {
                    echo "this deploy stage"
                    sh 'docker build -t $DOCKER_IMAGE .'
                    sh 'docker stop $CONTAINER_NAME_DEPLOY || true'
                    sh 'docker rm $CONTAINER_NAME_DEPLOY || true'
                    sh 'docker run -p 5000:5000 --name $CONTAINER_NAME_DEPLOY $DOCKER_IMAGE'
                   
                  }
               }
    }
}

