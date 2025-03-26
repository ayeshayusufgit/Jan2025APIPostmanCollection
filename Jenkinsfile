pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage("Deploy to QA") {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Checkout') {
            steps {
                //git url: 'https://github.com/naveenanimation20/July2024PostmanCollections'
				git url: 'https://github.com/ayeshayusufgit/Jan2025APIPostmanCollection.git'
            }
        }

        stage('Pull Docker Image') {
            steps {
                //sh 'docker pull naveenkhunteta/gorestddtest:1.0' for mac machine
				bat 'docker pull ayeshayusuf/gorestddtest:3.0' //for windows machine
            }
        }

        stage('Run API Test Cases') {
            steps {
                //sh 'docker run -v $(pwd)/newman:/app/results naveenkhunteta/gorestddtest:1.0' for mac machine
				bat 'docker run -v %cd%/newman:/app/results ayeshayusuf/gorestddtest:3.0'
            }
        }

        stage('Publish HTML Extra Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'newman',
                    reportFiles: 'gorest.html',
                    reportName: 'HTML Extra API Report',
                    reportTitles: ''
                ])
            }
        }

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
