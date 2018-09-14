pipeline {
  agent any
  stages {
    stage('build') {
      steps {
            sh '''cd containerization-spring-with-helm
                docker build -t yunlzheng/spring-sample:$GIT_COMMIT .'''
      }
    }

    stage('push image') {
      steps {
        withDockerRegistry([credentialsId: 'dockerhub', url: '']) {
          sh 'docker push yunlzheng/spring-sample:$GIT_COMMIT'
        }
      }
    }

    stage('public helm') {
      steps {
        data = readYaml(file: 'containerization-spring-with-helm/charts/values.yaml')
        data.image.tag = '0.0.1-$GIT_COMMIT'
      }
    }

  }
}
