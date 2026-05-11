pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/arnoggg/devops-158-GloorArno-tp'
            }
        }
        stage('Pull latest code') {
            steps {
                dir('/home/arno158/devops-158-ArnoGloor-tp') {
                    git branch: 'main', url: 'https://github.com/arnoggg/devops-158-GloorArno-tp'
                }
            }
        }
        stage('Install dependencies') {
            steps {
                dir('/home/arno158/devops-158-ArnoGloor-tp') {
                    sh '''
                        source venv/bin/activate
                        pip install flask
                    '''
                }
            }
        }
        stage('Restart Flask app') {
            steps {
                script {
                    sh 'pkill -f "python app.py" || true'
                    sh '''
                        cd /home/arno158/devops-158-ArnoGloor-tp
                        source venv/bin/activate
                        nohup python app.py > flask.log 2>&1 &
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Deploiement reussi'
        }
        failure {
            echo 'Echec du pipeline'
        }
    }
}
