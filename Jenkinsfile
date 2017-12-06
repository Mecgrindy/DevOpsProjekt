pipeline {
    agent any
    stages{
        stage("Checkout"){
            steps{
                git url: "https://github.com/Mecgrindy/devopsProjekt.git"
            }
        }
        stage("Packaging"){
            steps{
                sh "./gradlew build"
            }
        }
        stage("Docker build"){
            steps{
                sh "docker build -t grindy/devopsProjekt ."
            }
        }
        stage("Docker login"){
            steps{
                sh "docker login --username=grindy --password=$docker_password"
            }
        }
        stage("Docker push"){
            steps{
                sh "docker push grindy/devopsProjekt"
            }
        }
        stage("Deploy to Production"){
            steps{
                sh "ansible-playbook playbook.yml -i inventory/production"
            }
        }
    }
}
