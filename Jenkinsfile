pipeline {
    agent any

    tools {
        nodejs "nodejs"   // matches the NodeJS installation name
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
                // sanity checks
                sh 'node -v'
                sh 'npm -v'
                sh 'npm run lint || echo "No lint step defined, skipping..."'
            }
        }

        stage('Deploy to Render') {
            steps {
                // Replace this with your actual Render Deploy Hook
                sh 'curl -X POST https://api.render.com/deploy/srv-d37rsh8gjchc73cha5gg?key=lt2ylZma3wY'
            }
        }
    }
}
