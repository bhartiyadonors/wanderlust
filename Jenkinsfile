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
                    docker_build("wanderlust-frontend","3.2","madhupdevops","frontend")
                }
            }
        }

        stage("Docker: Backend Dockerization"){
            steps{
                script{
                    docker_build("wanderlust-backend","3.2","madhupdevops","backend")
                }
            }
        }

        stage("Docker: Pushing to DockerHub"){
            steps{
                script{
                    docker_push("wanderlust-frontend","3.2","madhupdevops")
                    docker_push("wanderlust-backend","3.2","madhupdevops")
                }
            }
        }

        stage("Docker: Artifact Cleanup"){
            steps{
                script{
                    docker_cleanup("wanderlust-frontend","3.2","madhupdevops")
                    docker_cleanup("wanderlust-backend","3.2","madhupdevops")
                }
            }
        }

        stage("Trigger CD Pipeline") {
            steps {
                script {
                    sh "curl -v -k --user admin:${JENKINSAPI} -X POST -H 'cache-control: no-cache' -H 'content-type: application/x-www-form-urlencoded' '20.193.134.140:8080/job/Wanderlust-CD/'"
                }
            }
        }
      }
}
