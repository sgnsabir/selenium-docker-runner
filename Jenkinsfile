pipeline{
    agent any
    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'BROWSER'
    }
    
    stages{

        stage('Start Grid'){
            steps{
                sh "sudo rm -rf output"
                sh "sudo docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
            }
        }

        stage('Run Test'){
            steps{
                sh "sudo docker-compose -f test-suites.yaml up"
            }
        }
    }

    post{
        always{
            sh "sudo chmod 777 -R output"
            sh "sudo docker-compose -f grid.yaml down"
            sh "sudo docker-compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}