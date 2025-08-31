pipeline{
  agent any
  tools{
    maven 'Maven3'
    jdk 'Java17'
  }

  environment{
    DOCKER_HUB_USER='manogaonkar'
    DOCKER_HUB_REPO='java-app'
    BUILD_NUMBER='latest'
  }
  
  stages{
    stage('checkout'){
      steps{
        
        script{
          def username = 'Manoj'
          echo "Hello Mr. ${username}"
        }
        
        withCredentials([string(credentialsId: 'secretText', variable: 'MY_SECRET')]){
          echo "This is my secret text $MY_SECRET"
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

    // stage('Archive Artifact'){
    //   steps{
    //     archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
    //   }
    // }

    stage('Docker Build'){
      steps{
        sh 'docker build -t $DOCKER_HUB_USER/$DOCKER_HUB_REPO:$BUILD_NUMBER .'
      }
    }

    stage('Docker Push'){
      steps{
        withCredentials([usernamePassword(credentialsId: 'dockerHubCred', usernameVariable: 'USER', passwordVariable: 'PASS')]){
          sh 'docker login -u $USER -p $PASS'
          sh 'docker push -t $DOCKER_HUB_USER/$DOCKER_HUB_REPO:$BUILD_NUMBER'
        }
      }
    }
    
  }
}
