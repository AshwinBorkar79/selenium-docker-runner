pipeline{

    agent any

    stages{

        stage('Start Selenium Grid'){
            steps{
                bat "docker-compose -f selenium-grid.yaml up -d"
            }
        }

        stage('Run Tests'){
            steps{
                bat "docker-compose -f test-suite.yaml up"
            }
        }
    }

    post {
        always {
            echo 'Stopping Selenium Grid & test-suites container...'
            bat "docker-compose -f selenium-grid.yaml down"
            bat "docker-compose -f test-suite.yaml down"

        }
    }
}