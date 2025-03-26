pipeline {
    agent any
     environment {
       
        AZURE_RESOURCE_GROUP = "learn-88f7a7b8-bde7-4992-8916-a4028634615f"
        AZURE_FUNCTION_APP = "myAzureFunctionApp2"
    }

    stages {
        stage('Check Azure Login') {
            steps {
                sh 'az account show'
            }
        }

        stage('Setup Python Virtual Environment') {
            steps {
                script {
                    sh '''
                    /bin/bash -c "python3 -m venv venv && source venv/bin/activate"
                    '''
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                    /bin/bash -c "source venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt"
                    '''
                }
            }
        }

        stage('Package Function') {
            steps {
                script {
                    sh '''
                    /bin/bash -c "source venv/bin/activate && zip -r functionapp.zip ."
                    '''
                }
            }
        }

        stage('Deploy to Azure') {
            steps {
                script {
                    sh '''
                    /bin/bash -c "source venv/bin/activate && az functionapp deployment source config-zip \
                        --resource-group learn-88f7a7b8-bde7-4992-8916-a4028634615f \
                        --name myAzureFunctionApp2 \
                        --src functionapp.zip"
                    '''
                }
            }
        }
    }
}
