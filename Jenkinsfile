
pipeline {
    agent any
    
    tools {
        jdk 'JDK25'  // Must match the JDK name configured in Jenkins Tools
    }
    
    stages {
        stage('Hello') {
            steps {
                echo 'Pipeline started!'
                echo "Build number: ${env.BUILD_NUMBER}"
                echo "Building on: ${env.NODE_NAME}"
            }
        }
        
        stage('Checkout') {
            steps {
                // The checkout happens automatically when using "Pipeline script from SCM"
                echo 'Code checked out from Git'
                git branch: 'main', url: 'https://github.com/251027-Java/trainer-code.git'
            }
        }
        
        stage('Build') {
            steps {
                // TODO: Complete this stage
                // 1. Make mvnw executable: sh 'chmod +x mvnw'
                // 2. Run Maven compile: sh './mvnw clean compile'
                echo 'Building the application...'
                sh 'cd ./W8/Kafka && chmod +x ./mvnw && ./mvnw clean install'
                dir('./W8/Kafka') {
                                    sh './mvnw package -DskipTests'
                                }
            }
        }
        
        stage('Test') {
            steps {
                // TODO: Complete this stage
                // Run Maven tests: sh './mvnw test'
                echo 'Running tests...'
                dir('./W8/Kafka') {
                sh './mvnw test'}
            }
        }
        
        stage('Package') {
            steps {
                // TODO: Complete this stage
                // Create JAR file: sh './mvnw package -DskipTests'
                echo 'Packaging JAR...'
                dir('./W8/Kafka') {
                sh './mvnw package -DskipTests'}
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline completed successfully!'
            echo "Artifact: target/*.jar"
        }
        failure {
            echo '❌ Pipeline failed! Check the logs above for errors.'
        }
        always {
            echo 'Pipeline finished.'
        }
    }
}
