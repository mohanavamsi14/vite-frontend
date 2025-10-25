pipeline {
    agent any

    environment {
        BUILD_DIR = "dist"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Repository cloned successfully"
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: "${BUILD_DIR}/**", fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                bat 'npx serve -s dist -l 5000'
                echo "Frontend deployed on port 5000"
            }
        }
    }

    post {
        success {
            echo "✅ Build and deployment completed!"
        }
        failure {
            echo "❌ Build failed. Check console output."
        }
    }
}
