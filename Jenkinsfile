pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/nguyen-anh-hao/spring-petclinic-microservices.git',
                        credentialsId: 'github-token'
                    ]]
                ])
            }
        }

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
            githubNotify context: 'CI', status: 'SUCCESS', description: 'Tests passed!'
        }
        failure {
            githubNotify context: 'CI', status: 'FAILURE', description: 'Tests failed!'
        }
    }
}
