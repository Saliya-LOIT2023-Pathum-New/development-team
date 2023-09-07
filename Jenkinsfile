pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from your GitHub repository and specific branch
                git(url: 'https://github.com/Saliya-LOIT2023-Pathum-New/development-team.git', branch: 'feat/newName1')
            }
        }



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

        stage('Build Docker Image') {
            steps {
               
                script {
                    docker.build('pathumra/welcome-loit-demo:latest')
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Push Docker image to Docker Hub
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        docker.image('pathumra/welcome-loit-demo:latest').push()
                    }
                }
            }
        }



        stage('Post build step') {
            steps {
                writeFile(file: 'status.txt', text: 'Welcome-LOIT')
            }
        }
    }
}

