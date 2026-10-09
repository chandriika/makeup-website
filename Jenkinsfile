
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate Files') {
            steps {
                sh '''
                    test -f index.html
                    test -f style.css
                    echo "Website files verified"
                '''
            }
        }

        stage('Deploy Nginx') {
            steps {
                sh '''
                    docker compose pull nginx
                    docker compose up -d
                '''
            }
        }

        stage('Verify Website') {
            steps {
                sh '''
                    docker compose ps
                    curl --fail http://localhost:2611/
                '''
            }
        }
    }

    post {
        success {
            echo 'Website deployed successfully using Nginx!'
        }
        failure {
            echo 'Deployment failed. Check the console output.'
        }
    }
}
