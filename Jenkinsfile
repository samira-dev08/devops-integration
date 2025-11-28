pipeline{
    agent any
    tools {
        maven 'maven-3.9.11'
    }
    stages{
        stage('build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/samira-dev08/devops-integration']])
                bat 'mvn clean install'
            }
        }
        stage('build Docker image'){
            steps{
                script{
                    bat 'docker build -t samira08/devops-integration .'
                }
            }
        }
        stage('push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubsecretkey')]) {
                       bat 'docker login -u samira08 -p %dockerhubsecretkey%'
}
                  bat 'docker push samira08/devops-integration'
                }
            }
        }
    }
}