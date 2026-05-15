pipeline {
    agent any

    tools {
        maven 'Maven-3'
        jdk 'JDK-21'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Code checkout completed from GitHub'
            }
        }

        stage('Check Java and Maven') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
                sh 'echo JAVA_HOME=$JAVA_HOME'
                sh 'echo MAVEN_HOME=$MAVEN_HOME'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Show Build Output') {
            steps {
                echo 'Checking generated artifact...'
                sh 'ls -lh target/'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running Java application...'
                sh 'java -cp target/jenkins-java-demo-1.0.0.jar com.demo.App'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline failed. Please check the Jenkins console logs.'
        }
    }
}
