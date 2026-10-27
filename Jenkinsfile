pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning repository...'

                git branch: 'main',
                    url: 'https://github.com/harini-sundari/week5.git'
            }
        }

        stage('Setup JUnit') {
            steps {
                echo 'Setting up JUnit...'

                sh '''
                    curl -L -o junit-platform-console-standalone.jar \
                    https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.10.2/junit-platform-console-standalone-1.10.2.jar
                '''
            }
        }

        stage('Compile') {
            steps {
                echo 'Compiling Java files...'

                sh '''
                    javac -cp junit-platform-console-standalone.jar \
                    Factorial.java FactorialTest.java
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running JUnit tests...'

                sh '''
                    java -jar junit-platform-console-standalone.jar \
                    --class-path . \
                    --scan-class-path
                '''
            }
        }

        stage('Run') {
            steps {
                echo 'Running Factorial application...'

                sh 'java Factorial'
            }
        }

        stage('Package JAR') {
            steps {
                echo 'Creating JAR file...'

                sh '''
                    jar cfm factorial.jar Manifest.txt Factorial.class
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                sh '''
                    mkdir -p deployment
                    cp factorial.jar deployment/
                '''
            }
        }

        stage('Archive JAR') {
            steps {
                echo 'Archiving JAR artifact...'

                archiveArtifacts artifacts: 'factorial.jar',
                                 fingerprint: true
            }
        }
    }

    post {

        success {
            echo 'CI/CD pipeline completed successfully!'
            echo 'Build, test, run, package and deployment successful.'
        }

        failure {
            echo 'CI/CD pipeline failed!'
        }
    }
}