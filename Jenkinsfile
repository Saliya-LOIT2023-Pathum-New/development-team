pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
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

        stage('Post build step') {
            steps {
                writeFile(file: 'status.txt', text: 'Welcome-LOIT')
            }
        }
    }
}
