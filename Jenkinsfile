pipeline {
  agent any
  stage('Build image') { // build and tag docker image
        steps {
            echo 'Starting to build docker image'

            script {
                def dockerfile = 'Dockerfile'
                def customImage = docker.build('http://ec2-18-180-155-162.ap-northeast-1.compute.amazonaws.com:8081/docker-virtual/hello-world:latest', "-f ${dockerfile} .")

            }
        }
    }
      
      stage ('Push image to Artifactory') { // take that image and push to artifactory
        steps {
            rtDockerPush(
                serverId: "artifactory-server",
                image: "http://ec2-18-180-155-162.ap-northeast-1.compute.amazonaws.com:8081/docker-virtual/hello-world:latest",
                host: 'tcp://localhost:2375',
                targetRepo: 'local-repo', // where to copy to (from docker-virtual)
                // Attach custom properties to the published artifacts:
                properties: 'project-name=docker1;status=stable'
            )
        }
    }
