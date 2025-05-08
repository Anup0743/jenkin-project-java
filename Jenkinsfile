pipeline {
    agent any
 tools {
        maven 'Maven 3.8.6' // name must match the one set above
    }
    stages {
        stage('version') {
            steps {
                bat 'mvn --version'
            }
        }

        stage('clean') {
            steps {
                bat 'mvn clean'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn package'
            }

            
        }
    }
}
