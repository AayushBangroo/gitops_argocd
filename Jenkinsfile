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
    }
}