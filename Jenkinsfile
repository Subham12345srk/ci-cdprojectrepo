pipeline{
    agent{
        node{
            label "JenkinsSlaveNodeLabel" 


        }
    }s
    stages{
        stage("checkout code stage"){
            steps{
                git url: "https://github.com/Subham12345srk/ci-cdprojectrepo.git",branch: "main"
            }
        }

        stage("Build Docker images"){
            steps{
                sh 'docker build -t myimage .'

            }
        }
        stage("push image to Dockerhub Stage"){
            steps{
                 withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'

                sh 'docker tag myimage djsubha/myimage'

                sh 'docker push djsubha/myimage'
                 }

            
            }
        }
        stage("Deploy to kubernetes"){
            steps{
                sh 'kubectl apply -f my-deployment.yml'
            }
        }

    }
}