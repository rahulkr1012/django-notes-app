@Library("Shared") _
pipeline{
    agent { label "rahul"}
    
    stages{
        
        stage("code") {
            steps {
                echo "code cloning suucess"
                git url: "https://github.com/rahulkr1012/django-notes-app.git", branch:"master"
            }
        }    
        stage(" build") {
            steps {
                echo "this will build the code"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("push") {
            steps {
                withCredentials([usernamePassword(credentialsId:"ef8e74a3-8165-4f0e-9ab4-53c0b46576b9",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                echo "code pushed to docker hub"
                 
                    
                }
            }
        }    
        stage("deploy") {
            steps {
                echo "deploy the code"
                sh "docker-compose up -d"
            } 
        }    
    }
}
