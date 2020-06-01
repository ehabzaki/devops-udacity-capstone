pipeline{ agent any
  stages {
    stage('Lint HTML.'){
      steps{
        sh 'tidy -q -e *.html'
      }
    }
    stage('Build image'){
      steps{
        sh 'docker build -t my-app .'
      }
    }
  }
}
