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
                    sh 'sudo docker run -d --name My-first-containe21211 -p 8085:8082 nandansaha0807/staragileprojectfinance:v1'
                }
            }
        }
    }
}
