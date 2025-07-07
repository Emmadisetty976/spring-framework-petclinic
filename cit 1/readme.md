pipeline {
    agent any
    stages{
        stage ('clone'){
            
        steps{
            git branch: 'main', url: 'https://github.com/Emmadisetty976/spring-petclinic.git'
        }
     }
      stage('build'){
        steps{
            sh 'mvn clean install'
        }
     }
      stage('test'){
       steps{
           sh 'mvn test'
       }
     }
      stage('test result '){
        steps{
           junit stdioRetention: 'ALL', testResults: 'target/surefire-reports/*.xml'       
           }
      }
      stage('published archiveArtifacts '){
        steps{
           archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
        }
      }
    }
}
