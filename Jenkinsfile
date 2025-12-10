pipeline {
    agent any

    tools {
        maven 'Maven3'   // configure this name in Jenkins Tools
        jdk 'JDK17'      // configure this name in Jenkins Tools
    }

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build (skip tests)') {
            steps {
                sh "mvn -B clean package -DskipTests"
            }
        }

        stage('Archive Jar') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        // ---------- LATER ----------
        // SonarQube stage goes here
        // Docker build/push stages go here
        // Kubernetes deploy stage goes here
        // ---------------------------
    }

    post {
        success {
            echo "✅ Build succeeded (tests skipped)"
        }
        failure {
            echo "❌ Build failed"
        }
        always {
            cleanWs()
        }
    }
}

