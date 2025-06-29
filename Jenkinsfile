pipeline {
    agent { label "Jenkins-agent" }
    environment{
        APP_NAME ="java-app-pipeline"
    }
    stages {
        stage('Cleanup Workspace') {
            steps {
                echo 'Cleaning up workspace...'
                cleanWs()
            }
        
            
        }
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/koushik2316/Gitops-manifests.git'
            }
        }
        stage('Update the deployment Tags') {
            steps {
                echo 'Updating deployment tags...'
                sh """
                   cat deployment.yaml
                   sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                   cat deployment.yaml
                """
                }
            }
        }
        // stage('Push the changes to Git') {
        //     steps {
        //         echo 'Pushing changes to Git...'
        //         sh """
        //            git config --global user.name "koushik2316"
        //            git config --global user.email "koushiknagendra2316@gmail.com"
        //            git add deployment.yaml
        //            git commit -m "Updated Deployment Manifest"
        //         """
        //         withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
        //           sh "git push https://github.com/koushik2316/gitops-register-app main"
        //         }
        //     }
        // }
    }



