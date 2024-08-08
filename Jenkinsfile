pipeline{
    agent any
    
    stages{

        stage('permission'){
            sh "sudo chmod 777 -R ."
        }

        stage('Start Grid'){
            steps{
                sh "sudo docker-compose -f grid.yaml up -d"
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
            sh "sudo docker-compose -f grid.yaml down"
            sh "sudo docker-compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}