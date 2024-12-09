pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'    // Ensure Java17 is correctly configured in Global Tool Configuration
        maven 'Maven 3'  // Use the exact tool name configured in Global Tool Configuration
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()  // Clean the workspace before starting
            }
        }
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'githun', url: 'https://github.com/sravankumardsk46/register-app'
            }
        }
        stage("Build Application") {
            steps {
                sh "mvn clean package"  // Build the project using Maven
            }
        }
        stage("Test Application") {
            steps {
                sh "mvn test"  // Run unit tests
            }
        }
    }
}
