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

        stage('Run Tests') {
            steps {
                script {
                    try {
                        sh 'npm test'
                    } catch (err) {
                        // Fail the build if tests fail
                        currentBuild.result = 'FAILURE'

                        // Optional: send email
                        emailext (
                            subject: "Jenkins Build Failed: ${env.JOB_NAME}",
                            body: "Tests failed. Check the console output at ${env.BUILD_URL}",
                            to: "youremail@example.com"
                        )

                        // Re-throw to mark build as failed
                        throw err
                    }
                }
            }
        }

        stage('Deploy to Render') {
            steps {

                sh 'curl -X POST https://api.render.com/deploy/srv-d37rsh8gjchc73cha5gg?key=lt2ylZma3wY'
            }
        }
    }
}
