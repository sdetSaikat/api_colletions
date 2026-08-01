pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage('Deploy to QA') {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/sdetSaikat/api_colletions'
            }
        }

        stage('Pull Docker Image') {
            steps {
                sh 'docker pull sdetsaikat/gorestddtest:1.0'
            }
        }

        stage('Run API Test Cases') {
            steps {
                sh 'docker run -v $(pwd)/newman:/app/results sdetsaikat/gorestddtest:1.0'
            }
        }

        stage('Publish HTML Extra Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'newman',
                    reportFiles: 'gorestdd.html',
                    reportName: 'HTML Extra API Report',
                    reportTitles: ''
                ])
            }
        }

        stage('Deploy to PROD') {
            steps {
                echo "Deploying to PROD"
            }
        }

    }

}
