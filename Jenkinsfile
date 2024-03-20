pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'server' 
    }
   stages {
        stage('Compilar') {
            steps {
                sh './gradlew build'
                sh './gradlew test' 
            }
        }
   }
}
