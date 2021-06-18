pipeline {
 agent {
  docker {
    args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
    image 'builder:v1.0'
    registryCredentialsId 'f27d57dd-5835-4003-b45a-b0598a851790'
    registryUrl 'http://35.214.18.4:8011'
    }
  } 
    stages {
        stage ('git clone') {
            steps {
                git 'https://github.com/veplotnikov/boxfuse.git' 
            }
        }
        
        stage ('maven artifact prepare') {
            steps {
              sh 'mvn package'
            }
        }
        
        stage ('Make Dockerfile') {
            steps {
              sh 'echo "FROM davidcaste/alpine-tomcat:jre8tomcat7" > Dockerfile && echo "ADD target/hello-1.0.war /opt/tomcat/webapps" >> Dockerfile'
            }
        }    
        
        stage ('build Prod') {
            steps {
                sh 'docker image build -t 35.214.18.4:8011/prod:v1.0 .'
            }    
        }
        
        stage ('push image') {
            steps {
                sh 'docker push 35.214.18.4:8011/prod:v1.0'
            }
        }
        
        
    }
}