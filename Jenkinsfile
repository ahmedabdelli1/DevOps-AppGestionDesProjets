pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }

        // ---------- BACKEND ----------
        stage('Compile Backend') {
            steps {
                dir('backend') {
                    sh 'mvn clean compile'
                }
            }
        }
        stage('Test Backend') {
            steps {
                dir('backend') {
                    sh 'mvn test'
                }
            }
        }
        stage('Package Backend') {
            steps {
                dir('backend') {
                    sh 'mvn package -DskipTests'
                }
            }
        }

        // ---------- FRONTEND ----------
        stage('Install Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                }
            }
        }
        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }

        // ---------- ARCHIVE ----------
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'backend/target/*.jar', fingerprint: true
            }
        }
    }
}
