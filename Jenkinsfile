pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
withCredentials([usernamePassword(credentialsId: 's', passwordVariable: 'password', usernameVariable: 'username')]) {
    

              sh "docker build -t zettblater/sharks:v$BUILD_ID ."
              sh "docker push zettblater/sharks:v$BUILD_ID"  }
            }
        }
     stage('Deploy') {
            steps {
              sh "docker run -d --name sharks-$BUILD_ID -p 80$BUILD_ID:8080 zettblater/sharks:v$BUILD_ID
            }
        }

    }
}
