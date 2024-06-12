pipeline{
    agent{
        label 'micro-service'
    }
    triggers{
        pollSCM('* * * * *')
    }
    environment{
        DOCKER_HUB_CREDENTIALS = credentials('docker_hub_PAT')
        IMAGE_NAME             = "lahari23/multi-containers"
        IMAGE_TAG              = "${env.BUILD_NUMBER}"
    }
    stages{
        stage('clone'){
            steps{
                git url: "https://github.com/lahari104/multi-branch.git",
                    branch: "qa"
            }
        }
        stage('build and deploy'){
            steps{
                sh 'docker build -t "${env.IMAGE_NAME}:${env.IMAGE_TAG}" .'
                sh 'echo ${DOCKER_HUB_CREDENTIALS_PSW} | docker login -u ${DOCKER_HUB_CREDENTIALS_USR} --password-stdin'
                sh 'docker container ls -a'
            }
        }
    }
}
