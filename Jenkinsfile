pipeline {
    agent any

    tools {
        maven 'Maven-3'
        jdk 'JDK-21'
    }

    environment {
        APP_NAME = 'jenkins-java-demo'
        DEPLOY_DIR = '/opt/jenkins-demo'
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Pulling latest code from GitHub...'
                checkout scm
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building application jar...'
                sh 'mvn clean package'
            }
        }

        stage('Show Build Output') {
            steps {
                echo 'Checking generated artifact...'
                sh 'ls -lh target/'
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application...'

                sh '''
                    mkdir -p ${DEPLOY_DIR}
                    cp target/${APP_NAME}-1.0.0.jar ${DEPLOY_DIR}/app.jar
                    echo "Application deployed to ${DEPLOY_DIR}"
                    ls -lh ${DEPLOY_DIR}
                '''
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running application for verification...'

                sh '''
                    cd ${DEPLOY_DIR}
                    java -jar app.jar
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Please check the Jenkins console logs.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}