pipeline {
    agent { label 'Jenkins-Agent' } // Specify the agent node
    tools {
        jdk 'Java17' // Ensure this matches the JDK name in Global Tool Configuration
        maven 'Maven3' // Ensure this matches the Maven name in Global Tool Configuration
    }
    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs() // Clean the workspace to avoid residue from previous builds
            }
        }
        stage("Checkout from SCM") {
            steps {
                // Clone the repository
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/sravankumardsk46/register-app'
            }
        }
        stage("Build Application") {
            steps {
                // Compile and package the application
                sh "mvn clean package"
            }
        }
        stage("Test Application") {
            steps {
                // Run tests
                sh "mvn test"
            }
        }
        stage("Debug Tools") {
            steps {
                // Print the versions of Java and Maven to verify setup
                sh "java -version"
                sh "mvn -version"
            }
        }
        stage("Archive Artifacts") {
            steps {
                // Archive the generated artifacts (e.g., JAR files)
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
    post {
        always {
            // Always display build logs and clean the workspace
            echo 'Pipeline finished.'
            cleanWs()
        }
        success {
            // Actions for successful builds
            echo 'Build succeeded.'
        }
        failure {
            // Actions for failed builds
            echo 'Build failed.'
        }
    }
}
