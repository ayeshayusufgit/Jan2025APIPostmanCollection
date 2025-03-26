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

        

        stage('Pull Docker Images') {
            parallel {
                stage('Pull GoRest Image') {
                    steps {
                        //sh 'docker pull naveenkhunteta/gorestddtest:1.0'
						bat 'docker pull ayeshayusuf/gorestddtest:3.0'
                    }
                }
                stage('Pull Booking Image') {
                    steps {
                        //sh 'docker pull naveenkhunteta/mybookingapi:1.0'
						bat 'docker pull naveenkhunteta/mybookingsapi:2.0'
                    }
                }
            }
        }

        stage('Prepare Newman Results Directory') {
            steps {
                //sh 'mkdir -p $(pwd)/newman'
				  bat 'mkdir -p %cd%/newman'
            }
        }

        stage('Run API Test Cases in Parallel') {
            parallel {
                stage('Run GoRest Tests') {
                    steps {
                        //sh 'docker run --rm -v $(pwd)/newman:/app/results naveenkhunteta/gorestddtest:1.0'
						bat 'docker run --rm -v %cd%/newman:/app/results ayeshayusuf/gorestddtest:3.0'
                    }
                }
                stage('Run Booking Tests') {
                    steps {
                        //sh 'docker run --rm -v $(pwd)/newman:/app/results naveenkhunteta/mybookingapi:1.0'
						bat 'docker run --rm -v %cd%/newman:/app/results ayeshayusuf/mybookingsapi:2.0'
                    }
                }
            }
        }

        stage('Publish HTML Extra Reports') {
            parallel {
                stage('Publish GoRest Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            //alwaysLinkToLastBuild: false,
							alwaysLinkToLastBuild: true,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'gorest.html',
                            reportName: 'GoRest API Report',
                            reportTitles: ''
                        ])
                    }
                }
                stage('Publish Booking Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            //alwaysLinkToLastBuild: false,
							alwaysLinkToLastBuild: true,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'bookings.html',
                            reportName: 'Booking API Report',
                            reportTitles: ''
                        ])
                    }
                }
            }
        }

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
