pipeline {
    agent any
    environment {
        SERVICE_CHANGED = sh(script: "git diff --name-only origin/main | grep -E 'customers-service|vets-service|visit-service' || echo ''", returnStdout: true).trim()
    }
    stages {
        stage('Test') {
            when {
                expression { return env.SERVICE_CHANGED != '' }
            }
            steps {
                echo "Running tests for changed services: ${env.SERVICE_CHANGED}"
                sh './mvnw test'
            }
        }
        stage('Build') {
            when {
                expression { return env.SERVICE_CHANGED != '' }
            }
            steps {
                echo "Building changed services: ${env.SERVICE_CHANGED}"
                sh './mvnw package -DskipTests'
            }
        }
    }
}
