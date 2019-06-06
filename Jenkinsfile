pipeline {
    agent {
        docker {
            image 'maven:3.3-jdk-8' 
            args '-v /root/.m2:/root/.m2' 
        }
    }

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'Maven_home') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'Maven_home') {
                    sh 'mvn test'
                }
            }
        }


        stage ('Package Stage') {
            steps {
                withMaven(maven : 'Maven_home') {
                    sh 'mvn package'
                }
            }
        }
		        
stage('Docker build') {
     steps {
      
          sh 'docker build -t javadock .'
		  
     }
}
        stage('Deploy') {
     steps {
 
          sh 'docker run -v /var/run/docker.sock:/var/run/docker.sock -d --rm -p 8765:8054 --name javadock'
		  
     }
}
	
    }
	
}

 
