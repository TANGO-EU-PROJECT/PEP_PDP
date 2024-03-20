pipeline {
     agent {
        node {
            label 'Agent01'
        }
    }
	tools {
          maven 'Maven-v.3.6.3'
          jdk 'jdk11.0'
    }
    environment {
        DOCKER_IMAGE = 'server' 
    }
   stages {
        stage('Compilar') {
            steps {
                dir('demo') {
		    sh 'java -version'
		    sh 'echo "JAVA_HOME=$JAVA_HOME"'
                    sh 'docker build -t server .'
		    sh 'docker run -e PDP_CONFIG=test -p 8088:8080 server'
                }
            }
        }
   }
}
