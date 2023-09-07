pipeline {
    agent any

    environment {
        dockerImage = ''
        registry = 'pathumra/welcome-loit-demo'
    }

    stages {
        stage('Check For POM') {
            steps {
                powershell '''if (Test-Path pom.xml) {
                    Write-Host "POM file exists"
                } else {
                    Write-Host "POM file does not exist"
                }'''
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Build Docker image') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }

        stage('Post build step') {
            steps {
                script {
                    try {
                        // Write "Welcome-LOIT" to a file named status.txt
                        writeFile(file: "${env.WORKSPACE}/status.txt", text: 'Welcome-LOIT')
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Failed to write status.txt: ${e.message}")
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Build and post-build steps completed successfully."
        }
        failure {
            echo "Build or post-build steps failed."
        }
    }
}
