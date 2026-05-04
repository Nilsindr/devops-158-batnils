pipeline {
    agent any

    triggers {
Modifié le: lundi 4 mai 2026, 08:15
        pollSCM('* * * * *')  // vérifie toutes les minutes
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nilsindr/devops-158-batnils/'
            }
        }

        stage('Pull latest code') {
            steps {
                dir('~/devops-158-batnils-tp') {
                    git branch: 'main', url: 'https://github.com/Nilsindr/devops-158-batnils/'
                }
            }
        }

        stage('Install dependencies') {
            steps {
                dir('~/devops-158-batnils-tp') {
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
                        cd ~/devops-158-batnils-tp
                        source venv/bin/activate
                        nohup python app.py > flask.log 2>&1 &
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Déploiement automatique réussi ! BRAVO DAMN'
        }
        failure {
            echo 'Échec du pipeline. - AIE AIE AIE CA PUE'
        }
    }
}

