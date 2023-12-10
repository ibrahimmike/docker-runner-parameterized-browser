pipeline{
    agent any
    parameters {
    choice choices: ['chrome', 'firefox'], description: 'Choose browser', name: 'BROWSER'
    }

    stages{
        stage('Start Grid'){
            steps{
              sh "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"

            }
        }
        stage('Bring Grid Down'){
            steps{

                sh "docker-compose -f test-suites.yaml up"

            }
        }
    }
    post{
        always{
          sh "docker-compose -f grid.yaml down"
          sh "docker-compose -f test-suites.yaml down"
        }
    }
}
