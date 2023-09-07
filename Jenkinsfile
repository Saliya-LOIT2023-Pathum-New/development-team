pipeline {
    agent any
	
	environment {
		dockerImage =''
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
                script{
					dockerImage = docker.build registry
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
