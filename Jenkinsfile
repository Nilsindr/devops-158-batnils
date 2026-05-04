pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nilsindr/devops-158-batnils/'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'bash -c "cd ~/devops-158-batnils-tp && source venv/bin/activate && pip install flask"'
            }
        }

        stage('Restart Flask app') {
            steps {
                script {
                    sh 'pkill -f "python app.py" || true'
                    sh 'bash -c "cd ~/devops-158-batnils-tp && source venv/bin/activate && nohup python app.py > flask.log 2>&1 &"'
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
