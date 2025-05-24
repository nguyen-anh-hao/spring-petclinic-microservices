pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'anhhao2004'
        COMMIT_ID = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm 
            }
        }

        stage('Build & Push Images') {
            steps {
                script {
                    // Danh sách các services cần build (dựa trên repo spring-petclinic-microservices)
                    def services = [
                        'admin-server',
                        'api-gateway',
                        'config-server',
                        'customers-service',
                        'discovery-server',
                        'vets-service',
                        'visits-service'
                    ]

                    // Lặp qua từng service để build và push
                    services.each { service ->
                        // Định nghĩa tag là COMMIT_ID
                        def containerTag = "${COMMIT_ID}"

                        // Thay đổi thư mục làm việc
                        sh "cd spring-petclinic-${service}"

                        // Build image bằng Maven profile và tag bằng COMMIT_ID
                        sh """./mvnw clean install -P buildDocker -Dmaven.test.skip=true \
                            -Ddocker.image.prefix=${DOCKER_REGISTRY} \
                            -Ddocker.image.tag=${containerTag}"""

                        // Push image lên Docker Hub
                        withDockerRegistry([credentialsId: 'dockerhub-credentials', url: '']) {
                            sh "docker push ${DOCKER_REGISTRY}/${service}:${containerTag}"
                        }

                        // Quay lại thư mục gốc
                        sh "cd .."
                    }
                }
            }
        }

        stage('Notify/Deploy') {
            steps {
                echo "All images pushed to Docker Hub with tag: ${COMMIT_ID}"
                // Có thể thêm webhook trigger ArgoCD tại đây
            }
        }
    }

    post {
        always {
            sh 'docker logout'  // Đảm bảo logout sau khi hoàn thành
        }
    }
}
