pipeline{
    agent {label: "dev");
    stages{
        stage("code"){
            steps{
                echo "Code is going to clone do it is a first stage"
                git url:"https://github.com/aruntsc/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
                echo "Code is now start to Build for project"
            }
        }
        stage("Test"){
            steps {
                echo "Code is now progress for Testing phase"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(
                credentialsId:"dockerhubCreds",
                passwordVariable: "dockerHubPass",
                usernameVariable: "dockerHubUser"
                )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build "
                echo "this is a final stage for deploying the app"
            }
        }
    }
        }
