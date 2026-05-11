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
                sh 'bash -c "cd $WORKSPACE && python3 -m venv venv && source venv/bin/activate && pip install flask pytest"'
            }
        }

        stage('Run unit tests') {
            steps {
                sh 'bash -c "cd $WORKSPACE && source venv/bin/activate && python -m pytest test_app.py -v --tb=short"'
            }
            post {
                success {
                    echo 'Tous les tests unitaires sont passés avec succès !'
                }
                failure {
                    echo 'Échec des tests unitaires. Le déploiement est annulé.'
                }
            }
        }

        stage('Restart Flask app') {
            steps {
                script {
                    sh 'pkill -f "python app.py" || true'
                    sh 'bash -c "cd $WORKSPACE && source venv/bin/activate && nohup python app.py > flask.log 2>&1 &"'
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
