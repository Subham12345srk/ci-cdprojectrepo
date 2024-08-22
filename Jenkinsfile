pipeline{
    agent{
        node{
            label "jenkinSlaveNodeLabel" 
            

        }
    }
    stages{
        stage("checkout code stage"){
            steps{
                git url "https://github.com/Subham12345srk/ci-cdprojectrepo.git",branch:"main"
            }
        }

        stage("Build Docker images"){
            steps{
                sh 'docker build -t myimage .'

            }
        }
        stage("push image to Dockerhub Stage"){
            steps{
                sh 'docker tag myimage djsubha/myimage'

                sh 'docker push djsubha/myimage'


            
            }
        }
        stage("Deploy to kubernetes"){
            steps{
                sh 'kubectl apply -f my-deployment.yml'
            }
        }

    }
}