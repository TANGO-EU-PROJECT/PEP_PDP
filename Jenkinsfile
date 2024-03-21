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
        DOCKER_IMAGE = 'server' 
    }
   stages {
        stage('Compilar') {
            steps {
                dir('demo') {
		    sh 'java -version'
		    sh 'echo "JAVA_HOME=$JAVA_HOME"'
			echo 'build gradle'
		    sh './gradlew build'
                   sh './gradlew test'
			 sh 'docker build -t server .'
		    sh 'docker run -e PDP_CONFIG=test -p 8088:8080 server'
                }
            }
        }
   }
}
