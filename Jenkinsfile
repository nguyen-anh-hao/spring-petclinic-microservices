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
                publishChecks name: 'CI', status: 'SUCCESS', description: 'Build successful', targetUrl: 'http://your-link-to-ci-report.com'
            }
        }

        failure {
            script {
                // Sử dụng publishChecks để gửi trạng thái thất bại về GitHub
                publishChecks name: 'CI', status: 'FAILURE', description: 'Build failed', targetUrl: 'http://your-link-to-ci-report.com'
            }
        }
    }
}
