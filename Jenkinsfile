pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "📥 Checking out code..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "🐍 Installing dependencies..."
                bat "python -m venv %VENV_DIR%"
                bat ".\\%VENV_DIR%\\Scripts\\pip install -r requirements.txt"
            }
        }

        stage('Run Tests') {
            steps {
                echo "🧪 Running tests..."
                bat ".\\%VENV_DIR%\\Scripts\\pytest --junitxml=report.xml"
            }
        }

        stage('Publish Report') {
            steps {
                echo "📊 Publishing JUnit report..."
                junit 'report.xml'
            }
        }
    }

    post {
        success {
            echo "✅ Tests passed!"
        }
        failure {
            echo "❌ Tests failed. See test report for details."
        }
    }
}
