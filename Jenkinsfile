pipeline {

  options {
    ansiColor('xterm')
  }

  agent {
    kubernetes {
      yamlFile 'builder.yaml'
    }
  }

  stages {

//     stage('Kaniko Build & Push Image') {
//       steps {
//         container('kaniko') {
//           script {
//             sh '''
//             /kaniko/executor --dockerfile `pwd`/Dockerfile \
//                              --context `pwd` \
//                              --destination=devopsinfotechumm/myweb:latest
//             '''
//           }
//         }
//       }
//     }

    stage('Deploy App to Kubernetes') {     
      steps {
        container('kubectl') {
          withKubeConfig([credentialsId: 'jenkins-kubernetes-default', serverUrl: 'https://10.10.11.232:6443']) {
            sh 'sed -i "s/<TAG>/latest/" myweb.yaml'
            sh 'kubectl apply -f myweb.yaml'
          }
        }
      }
    }
  }
}
