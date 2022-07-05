pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kingkarthikg/devops-auto']]])
                 bat "mvn clean install"

            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    bat 'docker build -t kingkarthikg/devops-integration .'
                }
            }
        }
        stage('Push image to hub'){
                steps{
                   script{
                        withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerpwd')]) {
                           bat 'docker login -u kingkarthikg -p ${dockerhubpwd}'
                           bat 'docker push kingkarthikg'
                        }
                   }
              }
        }
    }

}