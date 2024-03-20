pipeline {
    agent any
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        DOCKER_IMAGE = 'server' 
    }
   stages {
        stage('Compilar') {
            steps {
                dir('demo') {
                    sh 'java -version'
		            sh 'echo "JAVA_HOME=$JAVA_HOME"'
                    sh './gradlew build'
                    sh './gradlew test' 
                }
            }
        }
   }
}
