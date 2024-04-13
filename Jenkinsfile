pipeline {
    agent {
        node {
            label 'built-in'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                withMaven(maven: 'maven3') {
                    script {
                        if (isUnix()) {
                            sh 'mvn -Dmaven.test.failure.ignore clean package' // Execute Maven build (Unix)
                        } else {
                            bat 'mvn -Dmaven.test.failure.ignore clean package' // Execute Maven build (Windows)
                        }
                    }
                }
            }
        }
        stage('Results') {
            steps {
                junit '**/target/surefire-reports/TEST-*.xml' // Execute tests and generate JUnit reports
                archiveArtifacts 'target/*.jar' // Archive the built JAR file
            }
        }
    }
}
