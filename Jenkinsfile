pipeline {
    agent any

    environment {
        // Replace with your GitHub URL
        REPO_URL = 'https://github.com/varadsawantcodelab/zenkinsApp.git'
        DEST_DIR = '/var/www/html'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls the code from your repository
                checkout scmGit(
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: "${env.REPO_URL}"]]
                )
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Copy index.html to the web server directory
                    // Using sudo might require 'visudo' configuration for the jenkins user
                    sh "rm -rf ${env.DEST_DIR}/*"
                    sh "cp index.html ${env.DEST_DIR}/"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! Zenkins has updated your site.'
        }
        failure {
            echo 'Deployment failed. Check Jenkins logs for permission errors.'
        }
    }
}
