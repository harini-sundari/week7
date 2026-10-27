
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t week7 .'
            }
        }

        stage('Run') {
            steps {
                echo 'Running Flask application'
                sh 'docker rm -f mycontainer || true'
                sh 'docker run -d --name mycontainer -p 5001:5001 week7'
            }
        }
    }

    post {
        success {
            echo 'Flask Docker pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
