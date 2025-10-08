pipeline {
    agent any
    stages {
        stage('Install dependencies') {
            steps {
                echo "📦 Installing dependencies..."
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Run App') {
            steps {
                echo "🚀 Running Python App (main branch)"
                sh 'python3 app.py'
            }
        }
        stage('Run Tests') {
            steps {
                echo "🧪 Running Unit Tests"
                sh 'pytest test_app.py'
            }
        }
    }
    post {
        success {
            sh 'curl -H "Content-Type: application/json" \
                -X POST -d \'{"content": "✅ Build SUCCESS on *main* branch"}\' \
                https://discord.com/api/webhooks/1425459819413770261/9gv7psE61g9rJkNGwP3VgOJtnEB19tiRRqzjH8uP5llA8viXPk6KkEHlKrRunr0bfxYo'
        }
        failure {
            sh 'curl -H "Content-Type: application/json" \
                -X POST -d \'{"content": "❌ Build FAILED on *main* branch"}\' \
                https://discord.com/api/webhooks/1425459819413770261/9gv7psE61g9rJkNGwP3VgOJtnEB19tiRRqzjH8uP5llA8viXPk6KkEHlKrRunr0bfxYo'
        }
    }
}
