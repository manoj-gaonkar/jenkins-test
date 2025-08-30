pipeline{
  agent any
  tools{
    maven 'Maven3'
    jdk 'Java17'
  }
  
  stages{
    stage('checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/manoj-gaonkar/jenkins-test.git'
        }
    }
    
    stage('build'){
      steps{
        echo "Hello Building"
        sh 'mvn clean package'
      }
    }

    stage('test'){
      steps{
        sh 'mvn test'
      }
    }

    stage('Archive Artifact'){
      steps{
        archiveArtifacts artifacts: '**/target/*.jar', fingerpring: true
      }
    }
  }
}
