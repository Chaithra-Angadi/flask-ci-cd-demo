pipeline {
    agent any
    stages {
        stage('Clone') {
            steps { git 'https://github.com/Chaithra-Angadi/flask-ci-cd-demo.git' }
        }
        stage('Build') {
            steps { sh  'docker build -t flask-demo .' }
        }
        stage('Test') {
            steps {
                sh 'pip install pytest'
                sh 'pytest tests'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker tag flask-demo $USER/flask-demo:latest'
                    sh 'docker push $USER/flask-demo:latest'
                }
            }
        }
    }
}
