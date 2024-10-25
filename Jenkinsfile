@Library ("Shared") _
pipeline{
agent any
    stages{
    stage("Hello") {
        steps {
            script { hello ()
            }
        }
    }
    stage("code") {
        steps {
            script{
             clone ("<https://github.com/rahulkr1012/django-notes-app.git>", "master")
            }
        }
    }
    stage(" build") {
        steps {
            echo "this will build the code"
            script{
                docker_build("django-notes-app", "latest" , "rahulkr1796")
            }
        }
    }
    stage("push") {
        steps {
            script{
                docker_push("django-notes-app" ,"latest" , "rahulkr1796")
            }
            echo "code pushed to docker hub"
        }
    }
    stage("deploy") {
        steps {
            echo "deploy the code"
            sh "docker-compose up -d"
        }
    }
}

