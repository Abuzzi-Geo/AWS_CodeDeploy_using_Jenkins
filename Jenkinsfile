pipeline {
agent any

```
environment {
    AWS_DEFAULT_REGION = 'ap-south-2'
    APPLICATION_NAME = 'Abraham_App'
    DEPLOYMENT_GROUP = 'Demo-group'
    S3_BUCKET = 'abraham-codedeploy-demo-2026'
}

stages {

    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Create Artifact') {
        steps {
            sh '''
            zip -r deployment.zip .
            '''
        }
    }

    stage('Upload to S3') {
        steps {
            sh '''
            aws s3 cp deployment.zip s3://$S3_BUCKET/deployment.zip
            '''
        }
    }

    stage('Trigger CodeDeploy') {
        steps {
            sh '''
            aws deploy create-deployment \
            --application-name $APPLICATION_NAME \
            --deployment-group-name $DEPLOYMENT_GROUP \
            --s3-location bucket=$S3_BUCKET,bundleType=zip,key=deployment.zip \
            --region $AWS_DEFAULT_REGION
            '''
        }
    }
}
```

}
