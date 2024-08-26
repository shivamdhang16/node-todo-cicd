pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                echo 'Clone done'
                git url: "https://github.com/shivamdhang16/node-todo-cicd.git", branch: "master"
            }
        }
        stage('Build & Test') {
            steps {
                sh "docker build -t node-app-test-new ."
                echo 'Build & Test done'
            }
        }
        stage('Scan') {
            steps {
                echo 'Scanning done'
            }
        }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPass')]) {
                    sh '''
                    # Log in
                    echo "$dockerHubPass" | docker login -u "$dockerHubUser" --password-stdin
                    
                    # Tag
                    docker tag node-app-test-new:latest ${dockerHubUser}/node-app-test-new:latest
                    
                    # Push the Docker image to Docker Hub
                    docker push ${dockerHubUser}/node-app-test-new:latest
                    '''
                    echo 'Push done'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy done'
            }
        }
    }
}
