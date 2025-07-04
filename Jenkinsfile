pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6' // Name must match the one set in Jenkins Global Tools
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

    post {
        success {
            echo 'Build successful. Archiving and deploying...'

            // Archive WAR file
            archiveArtifacts artifacts: 'target/jenkin.war', fingerprint: true

            // Deploy WAR to Tomcat using curl
            bat """
                curl -u root:root ^
                --upload-file target/jenkin.war ^
                "http://localhost:8080/manager/text/deploy?path=/myapp&update=true"
            """
        }

        failure {
            echo 'Build failed. Deployment skipped.'
        }
    }
}
