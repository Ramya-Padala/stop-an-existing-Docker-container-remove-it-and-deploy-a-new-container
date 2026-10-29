pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git branch: 'main',
          url: 'https://github.com/Ramya-Padala/stop-an-existing-Docker-container-remove-it-and-deploy-a-new-container.git'
      }
    }
    stage('test docker iamge') {
      steps {
        sh '''
        docker ps -a
        docker stop <container_name>
        docker rm -f <container_id_or_name>
        '''
      }
    }
    stage('build docker image') {
      sh '''
     docker build -t my-apache-app .
     docker run -dit --name my-running-app -p 8086:80 my-apache-app
     '''
    }
  }
}
post {
        success {
            echo 'CI/CD pipeline completed successfully.'
            echo 'Open http://YOUR_SERVER_IP:8086'
        }

        failure {
            echo 'Pipeline failed. Check the Jenkins console output.'
        }

        always {
            sh 'docker rm -f apache-test >/dev/null 2>&1 || true'
        }
    }
  }
        
