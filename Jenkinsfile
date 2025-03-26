pipeline {
    agent any

    stages {
       

        stage('Setup Python Virtual Environment') {
            steps {
                sh '''
                python -m venv venv
                source venv/bin/activate
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                source venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Package Function') {
            steps {
                sh ''' source venv/bin/activate
                zip -r functionapp.zip .'''
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh '''
                 source venv/bin/activate
                az functionapp deployment source config-zip \
                    --resource-group learn-88f7a7b8-bde7-4992-8916-a4028634615f \
                    --name myAzureFunctionApp2 \
                    --src functionapp.zip
                '''
            }
        }
    }
}
