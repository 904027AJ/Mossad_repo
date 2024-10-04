pipeline {
    agent any

     tools {
        // Use the correct JDK version configured in Jenkins
        jdk 'jdk-17.0.12'  // Adjust to match your configuration
    }

    enviornment {
            SONARQUBE_SCANNER_HOME = tool 'SonarQubeScanner'
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the code from Git
                git branch: 'main', url: 'https://github.com/j2501/DeltaForce.git'
            }
        }

         stage('Compile') {
            steps {
                // Compile the Java file
                sh 'javac Assign.java'
            }
        }

        stage('SAST with SonarQube') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {  // Replace with your SonarQube server name
                    sh '''
                        ${SONARQUBE_SCANNER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=DeltaForce \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://localhost:9000
                    '''
                }
            }
        }
    

          stage('Run Application') {
            steps {
                // Run the compiled Java class
                sh 'java -cp . Assign'
            }
        }

        
        stage('Test') {
            steps {
                // If you have tests, you can add test steps here
                echo 'No tests to run for now'
            }
        }
}
     post {
        always {
            // Clean up or send notifications, if required
            echo 'Pipeline completed'
        }
        success {
            echo 'Pipeline completed successfully for Mossad'
        }
        failure {
            echo 'Pipeline failed for Mossad'
        }
    }
}
