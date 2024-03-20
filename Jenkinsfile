pipeline {
    agent any
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-1.17.0-openjdk-amd64'
        DOCKER_IMAGE = 'server' 
    }
   stages {
        stage('Compilar') {
            steps {
                dir('demo') {
                    sh 'docker build -t server .'
		    sh 'docker run -e PDP_CONFIG=test -p 8088:8080 server'
                }
            }
        }
   }
}
