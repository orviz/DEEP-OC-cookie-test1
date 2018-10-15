#!/usr/bin/groovy

Library(['github.com/indigo-dc/jenkins-pipeline-library']) _

pipeline {
    stages {
        stage('DockerHub delivery') {
            agent {
                label 'docker-build'
            }
            steps{
                checkout scm
                script {
                    image_id = DockerBuild(dockerhub_repo, env.BRANCH_NAME)
                }
            }
            post {
                success {
                    DockerPush(image_id)
                }
                failure {
                    DockerClean()
                }
                always {
                    cleanWs()
                }
            }
        }
    }
}
