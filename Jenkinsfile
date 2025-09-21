pipeline {
    agent any

    tools {
        nodejs "nodejs"   // must match the name you configured in Jenkins (Manage Jenkins → Global Tool Configuration)
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/Vusena/gallery.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Check') {
            steps {
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Deploy to Render') {
            steps {
                // Replace this with your Render Deploy Hook URL
                sh 'curl -X POST https://api.render.com/deploy/srv-xxxx?key=YOUR_DEPLOY_KEY'
            }
        }
    }
}
