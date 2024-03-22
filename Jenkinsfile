pipeline {
     agent {
        node {
            label 'Agent01'
        }
    }

	  tools {
          jdk 'jdk17.0'
    }
    environment {
	     APP_NAME = "test_module_rest"
        DOCKER_IMAGE = 'server' 
	ARTIFACTORY_SERVER = "harbor.tango.rid-intrasoft.eu"
      ARTIFACTORY_DOCKER_REGISTRY = "harbor.tango.rid-intrasoft.eu/tango/"
      BRANCH_NAME = "main"
      DOCKER_IMAGE_TAG = "$APP_NAME:R${env.BUILD_ID}"
    }
   stages {
        stage('Compile') {
            steps {
                dir('demo') {
		    sh 'java -version'
		    sh 'echo "JAVA_HOME=$JAVA_HOME"'
		    sh './gradlew build'
                }
            }
        }
	        stage('Build image') { // build and tag docker image
            steps {
		       dir('demo') {
                echo 'Starting to build docker image'
                script {
                    def dockerImage = docker.build(ARTIFACTORY_DOCKER_REGISTRY + DOCKER_IMAGE_TAG) 
                }
            }
	    }
        }

	stage("Push_Image"){
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'harbor-jenkins-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]){
                    echo "***** Push Docker Image *****"
                    sh 'docker login ${ARTIFACTORY_SERVER} -u ${USERNAME} -p ${PASSWORD}'
                    sh 'docker image push ${ARTIFACTORY_DOCKER_REGISTRY}${DOCKER_IMAGE_TAG}'
		    sh 'docker tag ${ARTIFACTORY_DOCKER_REGISTRY}${DOCKER_IMAGE_TAG} ${ARTIFACTORY_DOCKER_REGISTRY}${APP_NAME}:latest_dev'
		    sh 'docker image push ${ARTIFACTORY_DOCKER_REGISTRY}${APP_NAME}:latest_dev'
                }
            }
        }
	   stage("Run server"){
		    steps {
			     dir('demo') {
				    sh 'docker build -t server .'
				    sh 'docker run -e PDP_CONFIG=test -p 8088:8080 server'
				    }
		    }
	   }
   }
}
