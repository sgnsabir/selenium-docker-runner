pipeline{
    agent any
    
    stages{

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
        }
    }
}