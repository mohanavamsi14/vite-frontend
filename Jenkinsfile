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
                sh 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: "${BUILD_DIR}/**", fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh 'npx serve -s dist -l 5000 &'
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
