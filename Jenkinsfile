@Library('shared_lib') _

pipeline {
    agent {label 'slave1'}
    environment{
        SONAR_HOME = tool "Sonar"
    }
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

        stage('SonarQube: Code Analysis'){
            steps{
                script{
                    sonarqube_analysis("sonar","Wanderlust","Wanderlust")
                }
            }
        }

        stage("SonarQube: Quality Gates"){
            steps{
                script{
                    sonarqube_code_quality()
                }
            }
        }

        stage("Trivy: Filesystem scan"){
            steps{
                script{
                    trivy_scan()
                }
            }
        }

        stage("Docker: Frontend Dockerization"){
            steps{
                script{
                    docker_build("Wanderlust-backend","3.2","madhupdevops","frontend")
                }
            }
        }

        stage("Docker: Backend Dockerization"){
            steps{
                script{
                    docker_build("Wanderlust-backend","3.2","madhupdevops","backend")
                }
            }
        }

        stage("Docker: Pushing Frontend to DockerHub"){
            steps{
                script{
                    docker_push("Wanderlust-frontend","3.2","madhupdevops")
                }
            }
        }

        stage("Docker: Pushing Backend to DockerHub"){
            steps{
                script{
                    docker_push("Wanderlust-backend","3.2","madhupdevops")
                }
            }
        }
    }
}
