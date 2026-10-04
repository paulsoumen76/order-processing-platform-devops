pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout Application') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/paulsoumen76/order-processing-platform.git'
            }
        }

        stage('Build Order Service') {
            steps {
                sh './gradlew :order-service:clean :order-service:build -x test'
            }
        }
    }

    post {
        success {
            echo 'PR build PASSED'
        }

        failure {
            echo 'PR build FAILED'
        }
    }
}