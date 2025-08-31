pipeline{
  agent any
  tools{
    maven 'Maven3'
    jdk 'Java17'
  }
  
  stages{
    stage('checkout'){
      steps{
        
        script{
          def username = 'Manoj'
          echo 'Hello Mr. ${username}'
        }
        
        withCredentials([string(credentialsId: 'secretText', variable: 'MY_SECRET')]){
          sh "This is my secret text"
        }
        
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
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
      }
    }
  }
}
