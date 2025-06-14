pipeline{

    agent any

    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'BROWSER'
    }

    stages{

        stage('Start Selenium Grid'){
            steps{
                bat "docker-compose -f selenium-grid.yaml up --scale ${params.BROWSER}=2 -d"
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
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false

        }
    }
}