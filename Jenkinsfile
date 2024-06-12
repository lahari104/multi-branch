pipeline{
    agent{
        label 'micro-service'
    }
    triggers{
        pollSCM('* * * * *')
    }
    environment{
        // DOCKER_HUB_CREDENTIALS = credentials('docker_hub_PAT')
        IMAGE_NAME             = "lahari23/multi-containers"
        IMAGE_TAG              = "${env.BUILD_NUMBER}"
    }
    stages{
        stage('clone'){
            steps{
                git url: "https://github.com/lahari104/multi-branch.git",
                    branch: "develop"
            }
        }
        stage('build and deploy'){
            steps {
                sh """
                    docker build -t "${env.IMAGE_NAME}:${env.IMAGE_TAG}" .
                    docker push "${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                    docker run -d -P "${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                    docker container ls -a
                """
            }
        }
    }
}
