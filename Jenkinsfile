pipeline{ agent any
  stages {
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
