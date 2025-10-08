pipeline {
    agent any

    stages {
        stage('Setup Virtual Environment & Install dependencies') {
            steps {
                sh '''
                    echo "=== Membuat virtual environment ==="
                    python3 -m venv venv

                    echo "=== Aktivasi environment dan install dependencies ==="
                    . venv/bin/activate
                    venv/bin/pip install --upgrade pip
                    venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Run Feature App') {
            steps {
                echo "🚀 Running Python App (feature branch)"
                sh '''
                    . venv/bin/activate
                    venv/bin/python app.py &
                    sleep 3
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo "🧪 Running Tests"
                sh '''
                    . venv/bin/activate
                    venv/bin/python -m pytest -q test_app.py
                '''
            }
        }
    }

    post {
        success {
            sh '''
                echo "✅ Build SUCCESS — mengirim notifikasi ke Discord"
                curl -H "Content-Type: application/json" \
                    -X POST -d '{"content": "✅ Build SUCCESS on *feature* branch"}' \
                    https://discord.com/api/webhooks/1425459819413770261/9gv7psE61g9rJkNGwP3VgOJtnEB19tiRRqzjH8uP5llA8viXPk6KkEHlKrRunr0bfxYo
            '''
        }
        failure {
            sh '''
                echo "❌ Build FAILED — mengirim notifikasi ke Discord"
                curl -H "Content-Type: application/json" \
                    -X POST -d '{"content": "❌ Build FAILED on *feature* branch"}' \
                    https://discord.com/api/webhooks/1425459819413770261/9gv7psE61g9rJkNGwP3VgOJtnEB19tiRRqzjH8uP5llA8viXPk6KkEHlKrRunr0bfxYo
            '''
        }
    }
}
