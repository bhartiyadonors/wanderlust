@Library('shared_lib') _

pipeline {
    agent {label 'slave1'}
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Git: Code Checkout') {
            steps {
                script{
                    code_checkout()
                }
            }
        }
    }
}
