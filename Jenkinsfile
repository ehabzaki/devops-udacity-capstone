pipeline{ agent any
  stages {
    stage('Lint HTML.'){
      steps{
        sh 'tidy -q -e *.html'
      }
    }

    stage('Build image') {

        app = docker.build("capston")
    }

    stage('Push image') {
        docker.withRegistry('docker.io', '	docker_registry_cred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }

    stage('Deploying to EKS') {
        steps {
                dir('Kubernetes') {
                    withAWS(credentials: 'AWS_cred', region: 'us-east-2') {
                            sh " aws eks --region us-east-2 update-kubeconfig --name Capston-cluster"
                            sh 'kubectl get nodes'
                        }
                    }
            }
        }



  }
}
