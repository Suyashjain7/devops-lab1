pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code checked out successfully.'
            }
        }

        stage('Build') {
            steps {
                sh 'test -f index.html'
                sh 'mkdir -p build'
                sh 'cp index.html build/index.html'
                echo 'Build completed successfully.'
            }
        }

        stage('Test') {
            steps {
                sh "grep -qi "Welcome to my DevOps Project" build/index.html"
                echo 'Application test passed.'
            }
        }

        stage('Deploy') {
            steps {
                sh 'mkdir -p deploy'
                sh 'cp build/index.html deploy/index.html'
                echo 'Application deployed successfully.'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'deploy/**',
                             allowEmptyArchive: true,
                             fingerprint: true
        }

        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the build logs.'
        }
    }
}
