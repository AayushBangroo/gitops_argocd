pipeline{
    agent any

    environment{
        DOCKERHUB_USERNAME = "aayushbangroo"
        APP_NAME = "gitops-arogcd-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = 'dockerhub'
    }

    stages{
        stage("Cleanup Workspace"){
            steps{
                script{
                    cleanWs()
                }
            }
        }
        stage('Checkout SCM'){
            steps{
                script{
                    git credentialsId: 'github',
                    branch: 'master',
                    url: 'https://github.com/AayushBangroo/gitops_argocd.git'
                }
            }
        }
        stage('Build Docker image'){
            steps{
                script{
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
        stage('Docker Image Push'){
            steps{
                script{
                    docker.withRegistry('', REGISTRY_CREDS){
                        docker_image.push("$BUILD_NUMBER")
                        docker_image.push("latest")
                    }
                }
            }
        }
        stage('Delete Docker image'){
            steps{
                script{
                    sh "docker rm image ${IMAGE_NAME}:${IMAGE_TAG}"
                    sh "docker rm image ${IMAGE_NAME}:latest"
                }
            }
        }
    }
}
