pipeline{
    //agent any
    agent {label 'worker'}
    options{
        buildDiscarder(logRotator(daysToKeepStr: '7'))
        disableConcurrentBuilds()
        retry(3)
        timeout(time: 1, unit: 'MINUTES')
    }
    triggers {
        cron('H * * * *')
    }
    parameters{
        string(name: 'BRANCH', defaultValue: 'master', description: 'Enter branch')
        choice(name: 'OPERATION', choices: ['A', 'B', 'C'])
    }
    stages{
        stage('Initial'){
            steps{
                sh "echo hello C32"
            }
        }
        stage ('Parallel Stages'){
            parallel{
                stage('Unit testing'){
                    agent {label 'worker'}
                    steps{
                        sh "echo hello C32"
                        sh "sleep 120"
                    }
                }
                stage('UI testing'){
                    agent {label 'worker'}
                    steps{
                        sh "echo hello C32"
                        sh "sleep 120"
                    }
                }
            }
        }

    }
    post{
        always {
            echo "workspace cleanup"
            echo "docker rmi"
            echo "notifications"
        }
    }
}
