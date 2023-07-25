pipeline{
    agent{
        label "vagrant"
    }
    stages{
        stage("Git Pull"){
            steps{
                echo "======== Pulling Code from Github ========"
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sidpalas/mern-docker-compose.git']]])
            }
        }
        stage("Build Server"){
            steps{
                echo "======== Build Server ========"
                sh "cd server"
                sh "ls"
                sh "docker build -t api-server ."
            }
        }
        stage("Build Client"){
            steps{
                echo "======== Build Client ========"
                sh "cd client"
                sh "docker build -t react-app ."
            }
        }
        stage("Run Application"){
            steps{
                echo "======== Run Application ========"
                sh "docker-compose up -d"
            }
        }
    }
    post{
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}