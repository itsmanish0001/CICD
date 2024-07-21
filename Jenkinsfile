pipeline{
    agent any
    
    stages{
        stage("Clone code"){
            steps{
                echo "cloning the code"
                git url: "https://github.com/itsmanish0001/CICD.git", branch:"main"
            }
        }
        
        stage("build"){
             steps{
                echo "building the image"
                sh "docker build -t manish248/weather-app ."
            }
        }
        
        stage("push to dockerhub"){
             steps{
                echo "pushing image to docker hub"
                withCredentials([usernamePassword(credentialsId:"docker-credentials", passwordVariable:"dockerhubpass", usernameVariable:"dockerhubuser")]){
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                }
                
                sh "docker push manish248/weather-app:latest"
            }
        }
        
        stage("deploy"){
             steps{
                echo "deploying the application"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}