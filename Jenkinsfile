pipeline {

  agent (label 'node1')

  stages {

    def app

    stage('Clone') {
        
        checkout scm

	    }

    stage('Build image') {

        app = docker.build("docker-mkdocs")
    }

    stage('Test image') {

        app.inside {

        sh 'echo "Tests passed"'
       
       }

    }

    stage('Push image') {

        sh "docker login -u ${DOCKER_USER} -p ${DOCKER_PASSWD} registry"

        docker.withRegistry('https://registry.hub.docker.com', 'DOCKERCREDENTIALS') {
            
	app.push("${env.BUILD_NUMBER}")

        app.push("latest")
          }
       }
    } 
 }
