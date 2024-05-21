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
                    code_checkout("https://github.com/DevMadhup/wanderlust.git","feat-131-dockerize")
                }
            }
        }

        stage('SonarQube: Code Quality') {
            steps {
                script{
                    sonarqube_code_quality()
                }
            }
        }

        stage('SonarQube: Code Analysis') {
            steps {
                script{
                    sonarqube_analysis("sonar","Wanderlust","Wanderlust")
                }
            }
        }
    }
}
