pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Giả lập quá trình build
                    echo "Building..."
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Giả lập quá trình test
                    echo "Testing..."
                }
            }
        }
    }

    post {
        success {
            script {
                // Sử dụng publishChecks để gửi trạng thái thành công về GitHub
                publishChecks name: 'CI', status: 'SUCCESS', conclusion: 'SUCCESS'
            }
        }

        failure {
            script {
                // Sử dụng publishChecks để gửi trạng thái thất bại về GitHub
                publishChecks name: 'CI', status: 'FAILURE', conclusion: 'FAILURE'
            }
        }
    }
}
