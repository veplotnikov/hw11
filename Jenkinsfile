pipeline {
   
   agent { none 
     }
  
    stages {
        agent {
         docker {
           args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
           image 'builder:v1.0'
           registryCredentialsId 'f27d57dd-5835-4003-b45a-b0598a851790'
           registryUrl 'http://35.214.18.4:8011'
           }
        }
        stage ('git clone') {
        agent {
         docker {
           args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
           image 'builder:v1.0'
           registryCredentialsId 'f27d57dd-5835-4003-b45a-b0598a851790'
           registryUrl 'http://35.214.18.4:8011'
           }
        }
            steps {
               git 'https://github.com/veplotnikov/boxfuse.git' 
            }
        }
        
        stage ('maven artifact prepare') {
        agent {
         docker {
           args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
           image 'builder:v1.0'
           registryCredentialsId 'f27d57dd-5835-4003-b45a-b0598a851790'
           registryUrl 'http://35.214.18.4:8011'
           }
        }
            steps {
              sh 'mvn package'
            }
        }
        
        stage ('Make Dockerfile') {
        agent {
         docker {
           args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
           image 'builder:v1.0'
           registryCredentialsId 'f27d57dd-5835-4003-b45a-b0598a851790'
           registryUrl 'http://35.214.18.4:8011'
           }
        }
            steps {
              sh 'echo "FROM davidcaste/alpine-tomcat:jre8tomcat7" > Dockerfile && echo "ADD target/hello-1.0.war /opt/tomcat/webapps" >> Dockerfile'
            }
        }    
        
        stage ('build Prod') {
        agent {
         docker {
           args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
           image 'builder:v1.0'
           registryCredentialsId 'f27d57dd-5835-4003-b45a-b0598a851790'
           registryUrl 'http://35.214.18.4:8011'
           }
        }
            steps {
                sh 'docker image build -t 35.214.18.4:8011/prod:v1.0 .'
            }    
        }
        
        stage ('push image') {
        agent {
         docker {
           args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
           image 'builder:v1.0'
           registryCredentialsId 'f27d57dd-5835-4003-b45a-b0598a851790'
           registryUrl 'http://35.214.18.4:8011'
           }
        }
            steps {
                sh 'docker push 35.214.18.4:8011/prod:v1.0'
            }
        }
        
        
    }
}