pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './mvnw test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building application...'
                sh './mvnw package -DskipTests'
            }
        }
    }
}
