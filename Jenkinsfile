pipeline {
    agent any
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
                sh "docker login -u jayakavitha -p jk@1234567"
                sh '''
                    cd vote
                    docker build -t jayakavitha/vote:v${BUILD_NUMBER} .
                '''
                sh "docker push jayakavitha/vote:v${BUILD_NUMBER}"
            }
        }
        stage("deploy") {
            steps {
                sh "echo starting deployment"
            }
        }
    }
}
