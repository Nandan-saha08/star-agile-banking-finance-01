pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/Nandan-saha08/star-agile-banking-finance-01.git', branch: "master"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t nandansaha0807/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
         stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) { 
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
					sh 'docker push nandansaha0807/staragileprojectfinance:v1' 
                }
            }
        }
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-containe21211 -p 8083:8081 nandansaha0807/staragileprojectfinance:v1'
                  
                }
            }
        
    }
}
