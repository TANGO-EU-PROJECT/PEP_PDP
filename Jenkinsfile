pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'server' 
    }
   stages {
        stage('Compilar') {
            steps {
                dir('demo') {
                    sh './gradlew build'
                    sh './gradlew test' 
                }
            }
        }
   }
}
