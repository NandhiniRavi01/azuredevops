pipeline {
    agent any
     environment {
       
        AZURE_RESOURCE_GROUP = "learn-88f7a7b8-bde7-4992-8916-a4028634615f"
        AZURE_FUNCTION_APP = "myAzureFunctionApp2"
    }

    stages {
     stage('Azure Login') {
    steps {
        script {
            sh 'az login --use-device-code --allow-no-subscriptions'
        }
    }
}

        stage('Verify Azure Account') {
    steps {
        script {
            sh 'az account show'
        }
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
                    az account set --subscription c44007ce-0884-475d-8661-b6c607629ec4
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
