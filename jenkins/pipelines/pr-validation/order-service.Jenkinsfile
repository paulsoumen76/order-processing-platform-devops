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
                sh '''
                    chmod +x gradlew
                    ./gradlew :order-service:clean :order-service:build -x test
                '''
            }
        }
    }

    post {
        success {
            echo 'Order Service build PASSED'
        }

        failure {
            echo 'Order Service build FAILED'
        }
    }
}