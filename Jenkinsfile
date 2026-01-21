pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK11'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'master'
                    branch 'develop'
                }
            }
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            when {
                branch 'master'
            }
            steps {
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline successful for branch: ${env.BRANCH_NAME}"
        }
        failure {
            echo "❌ Pipeline failed for branch: ${env.BRANCH_NAME}"
        }
    }
}
