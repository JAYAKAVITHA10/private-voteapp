pipeline {
    agent {label 'worker'}
    options {
        buildDiscarder(logRotator(numToKeepStr: '15'))
        disableConcurrentBuilds()
        retry(2)
        timeout(time: 20, unit: 'MINUTES')
    }
    parameters {
        string( name: 'BRANCH', defaultValue: 'main', description: 'branch to build?')
        choice(name: 'ENV', choices: ['qa', 'dev', 'prod'],  description: 'env to build')
    }
    stages {
        stage("Docker login and push") {
            steps {
                sh "docker login -u <username> -p <password>"
                sh '''
                    cd vote
                    docker build -t yogesh010/vote:v${BUILD_NUMBER} .
                '''
                sh "docker push yogesh010/vote:v${BUILD_NUMBER}"
            }
        }
        stage("deploy") {
            steps {
                sh "echo starting deployment"
            }
        }
    }
}
