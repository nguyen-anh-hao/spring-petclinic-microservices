pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Trạng thái là "PENDING" khi build đang chạy
                    githubNotify context: 'CI', status: 'PENDING', description: 'Building...'
                }
                // Code build ở đây (ví dụ: Maven, NPM)
                echo "Building..."
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Sau khi build thành công
                    githubNotify context: 'CI', status: 'SUCCESS', description: 'Tests passed'
                }
                // Code test ở đây
                echo "Testing..."
            }
        }
    }

    post {
        success {
            script {
                // Trạng thái thành công
                githubNotify context: 'CI', status: 'SUCCESS', description: 'Build Successful'
            }
        }
        failure {
            script {
                // Trạng thái thất bại
                githubNotify context: 'CI', status: 'FAILURE', description: 'Build Failed'
            }
        }
    }
}
