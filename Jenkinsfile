pipeline {
    agent any

    stages {
       

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Package Function') {
            steps {
                sh 'zip -r functionapp.zip .'
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh '''
                az functionapp deployment source config-zip \
                    --resource-group learn-88f7a7b8-bde7-4992-8916-a4028634615f \
                    --name myAzureFunctionApp2 \
                    --src functionapp.zip
                '''
            }
        }
    }
}
