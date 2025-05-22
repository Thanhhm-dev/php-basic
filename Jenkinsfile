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
                sh 'docker run --rm my-php-node-app:latest php artisan test'
            }
        }

        stage('Push Image (optional)') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker tag my-php-node-app:latest mydockerhubuser/my-php-node-app:latest
                        docker push mydockerhubuser/my-php-node-app:latest
                    '''
                }
            }
        }
    }
}