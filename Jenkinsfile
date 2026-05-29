pipeline {
    agent any

    environment {
        APPLICATION_NAME = 'Abraham_App'
        DEPLOYMENT_GROUP = 'Demo-group'
        AWS_DEFAULT_REGION = 'ap-south-2'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Show Commit') {
            steps {
                sh 'git rev-parse HEAD'
            }
        }

        stage('Trigger CodeDeploy') {
            steps {
                sh '''
                aws deploy create-deployment \
                  --application-name $APPLICATION_NAME \
                  --deployment-group-name $DEPLOYMENT_GROUP \
                  --region $AWS_DEFAULT_REGION
                '''
            }
        }
    }
}