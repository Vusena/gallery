pipeline {
    agent any

    tools {
        nodejs "nodejs"
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
                sh 'npm run lint || echo "No lint step defined, skipping..."'
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    try {
                        sh 'npm test'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        emailext (
                            subject: "Jenkins Build Failed: ${env.JOB_NAME}",
                            body: "Tests failed. Check console output: ${env.BUILD_URL}",
                            to: "youremail@example.com"
                        )
                        throw err
                    }
                }
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
