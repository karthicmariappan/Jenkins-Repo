pipeline{
  agent any
  stages{
    stage('Build'){
      steps {
        echo 'Building the project'
      }
    }
    stage('Test') {
        steps {
            echo 'runnig the Code...'
        }
    }
    stage('Deploy') {
        step {
            echo 'Deploying the code'
        }
    }
  }
}