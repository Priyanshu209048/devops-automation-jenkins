pipeline {
    agent any
    tools{
        maven 'maven_3_9_10'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Priyanshu209048/devops-automation-jenkins']])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker image'){
            steps{
                script{
                    bat 'docker build -t priyanshubaral/devops-integration .'
                }
            }
        }
        stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        bat 'docker login -u priyanshubaral -p ${dockerhubpwd}'
                    }
                    bat 'docker push priyanshubaral/devops-integration'
                }
            }
        }
    }
}