pipeline {
    agent any
    environment {

    ANSIBLE_PRIVATE_KEY=credentials('ssh-key')
}
    stages {
        stage('Build') {
            steps {
withCredentials([usernamePassword(credentialsId: 's', passwordVariable: 'password', usernameVariable: 'username')]) {
    

              sh "docker build -t zettblater/sharks:v$BUILD_ID ."
              sh "docker push zettblater/sharks:v$BUILD_ID"  }
            }
        }
     stage('Deploy') {
            steps { withCredentials([usernamePassword(credentialsId: 's', passwordVariable: 'password', usernameVariable: 'username')]) {
              sh "ansible-playbook playbook.yaml -u ansiblo --private-key=$ANSIBLE_PRIVATE_KEY -e password=$password -e username=$username -e BUILD_ID=$BUILD_ID --become -i inventory" }
            }
        }

    }
}
