pipeline {
    agent any

    environment {
        AZURE_CREDENTIALS = credentials('AzureServicePrincipal')
        RESOURCE_GROUP = 'jenkins-get-started-rg'
        APP_NAME = 'meihuan-node-app-20260324'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Zip App') {
            steps {
                sh 'zip -r app.zip .'
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh '''
                az login --service-principal \
                  -u $AZURE_CREDENTIALS_USR \
                  -p $AZURE_CREDENTIALS_PSW \
                  --tenant 5c4dec6f-7dc8-4142-8d6b-af773cf5307e

                az webapp deployment source config-zip \
                  --resource-group $RESOURCE_GROUP \
                  --name $APP_NAME \
                  --src app.zip
                '''
            }
        }
    }
}
