pipeline {
    
    agent none
  
    stages {
        stage ('Build and push the Immage') {
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
               sh 'mvn package'
               sh 'echo "FROM davidcaste/alpine-tomcat:jre8tomcat7" > Dockerfile && echo "ADD target/hello-1.0.war /opt/tomcat/webapps" >> Dockerfile && echo "CMD [\"/opt/tomcat/bin/catalina.sh\",\"run\"]"  >> Dockerfile'
               sh 'docker image build -t 35.214.18.4:8011/prod:v1.1 .'
               sh 'docker push 35.214.18.4:8011/prod:v1.0'
            }
        }
        stage ('deploy') {
        agent any
        
            steps {
                sh 'docker run -p 8081:8080 35.214.18.4:8011/prod:v1.1'
            }
        }
        
        
    }
}