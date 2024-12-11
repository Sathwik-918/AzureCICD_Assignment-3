pipeline {
    agent any
    environment {
        AZURE_CLIENT_ID = credentials('azure-client-id')
        AZURE_CLIENT_SECRET = credentials('azure-client-secret')
        AZURE_TENANT_ID = credentials('azure-tenant-id')
        RESOURCE_GROUP = 'your-resource-group'
        FUNCTION_APP_NAME = 'your-function-app-name'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm install' // Adjust for Python or other languages
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test' // Replace with test command for your language
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to Azure...'
                sh """
                    az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
                    az functionapp deployment source config-zip --resource-group $RESOURCE_GROUP --name $FUNCTION_APP_NAME --src function.zip
                """
            }
        }
    }
}
