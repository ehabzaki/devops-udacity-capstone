pipeline{ agent any
  stages {
    stage('Lint HTML.'){
      steps{
        sh 'tidy -q -e *.html'
      }
    }
    stage('Upload to AWS.'){
      steps{
        withAWS(credentials: 'aws-static', region: 'us-east-2') {
        //sh 'aws iam get-user'
        s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'udagram-ehab', path:'index.html')
        }
      }
    }
  }
}
