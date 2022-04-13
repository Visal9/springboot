pipeline {
agent any
    environment{
    //Server_Credential = credentials('TEST_CRED')
   // registry = "http://us-central1-docker.pkg.dev/poetic-sentinel-343407/springboost"
        registry = "cloud.canister.io:5000/ima/springboot-test"
    registryCredential = 'DOCKER_REGISTERY'
    dckerImage =''
    }
    tools { 
        maven 'maven' 
    }
    
    
stages {
    stage("testing"){
        //we can use this for get credential in step level
           steps {
          echo "this is testing" 
         // withCredentials ([
           //   usernamePassword(credentialsId:'TEST_CRED',usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')
      //    ]) {
            //   echo "this is testing $USERNAME" 
           //    echo "this is from env variable $Server_Credential_USR"
           //   sh 'who'
        //  }

echo "testing"
               sh "who"
        }
    }
    
    
    
      stage("build"){
    
           steps {
               
         sh 'mvn clean package'
           
        }
    }
    
    
    
    stage('Building image') {
        steps{
            script {
            dockerImage = docker.build registry
            }
       }
    }
    
    
    stage('Deploy our image') {
steps{
script {
docker.withRegistry( 'https://cloud.canister.io:5000', registryCredential ) {
dockerImage.push()
}
}
  
}
}
stage('env') {
        // Jenkins provides no environment variable view
    steps{
        sh 'printenv|sort'
    }
    }
   
}
post {
    always {
        echo "this execte only fails"
    }
    success {
        echo "this execute only if command success"
    }
}
}
