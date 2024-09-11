pipeline {
    agent any

    stages {
        stage('Build Project') {
            steps {
                git url: 'https://github.com/Nandan-saha08/star-agile-banking-finance-01.git', branch: 'master'
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t nandansaha0807/staragileprojectfinance:v1 .'
                }
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) { 
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push nandansaha0807/staragileprojectfinance:v1'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Remove any existing container with the same name
                    sh 'docker rm -f Finance_Project_01 || true'
                    // Run the new container
                    sh 'docker run -d --name Finance_Project_01 -p 8083:8081 nandansaha0807/staragileprojectfinance:v1'
                }
            }
        }
    }
}
