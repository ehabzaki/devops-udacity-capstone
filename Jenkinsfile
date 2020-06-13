pipeline{ agent any
  stages {
    stage('Lint HTML.'){
      steps{
        sh 'tidy -q -e *.html'
      }
    }

    stage('Build image') {
      steps{
        script{
        app = docker.build("ehab123/capston")
        }
      }
    }

    stage('Push image') {
       steps{
        script{
        docker.withRegistry('', '	docker_registry_cred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        }
       }
    }

    stage('Deploying to EKS') {
        steps {
                  script{
                    withAWS(credentials: 'AWS_cred', region: 'us-east-2') {
                      sh "aws sts get-caller-identity"
                            sh " aws eks --region us-east-2 update-kubeconfig --name Capston-cluster"
                            sh 'kubectl get nodes'
                        
                    }
            }
            }
        }



  }
}
