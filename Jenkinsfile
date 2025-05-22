pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo '🐳 Build image cho PHP + Node app'

                // Build image với tag
                sh 'docker build -t my-php-node-app:latest .'
            }
        }

        stage('Run Tests in Container') {
            steps {
                echo '🧪 Chạy container test'

                // Chạy container để test Laravel bằng lệnh artisan test
                sh 'docker run --rm my-php-node-app:latest php test.php'
            }
        }
    }
}