pipeline{
  agent any
  stages{
    stage('checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/manoj-gaonkar/jenkins-test.git'
        }
    }
    stage('build'){
      steps{
        echo "Hello Building"
      }
    }
  }
}
