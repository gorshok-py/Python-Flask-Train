pipeline {
        options {
        buildDiscarder(
            logRotator(
                artifactDaysToKeepStr: "",
                artifactNumToKeepStr: "",
                daysToKeepStr: "",
                numToKeepStr: "10"
            )
        )
    }
    
    agent any
    
    stages {
        stage('Get Python Flask App') {
            steps {
                git branch: 'main', url: 'https://github.com/gorshok-py/Python-Flask-Train.git'
                  }
                                }   
        stage('Preparation build image') {
            steps {
            sh 'docker build -t python-flask-image .'
                                }
                                         }
        stage('Docker run Container') {
            steps {
            sh 'docker run -d --name pythonapplet -p 5001:8000 python-flask-image:latest'
                  }
                                         }
        stage('Test Connection') {
            steps {
            sh 'curl localhost:5001'
                  }
                                         }
        stage('Clean') {
            steps {
            sh 'docker stop pythonapplet'
            sh 'docker container rm pythonapplet'
                  }
                                         }
                                         
    }
            post {
            always {
                cleanWs()
        }
    }
}
