pipeline {
    agent any
    stages{
        stage("Code") {
            steps {
                git url: 'https://github.com/vibhishh/2048.git', branch: 'master'
            }
        }
        stage("Build And Test") {
            steps {
                sh 'docker build . -t mradulsingh25/2048-game:latest'
            }
        }
         stage("Login And push"){
            steps {
                echo "Logging in and pushing the image to dockerhub"
               withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push mradulsingh25/2048-game:latest"
                }
            }
        }
         stage("Deployed"){
            steps {
                sh 'docker-compose down && docker-compose up -d --no-deps --build web'
            }
        }
    }
}
