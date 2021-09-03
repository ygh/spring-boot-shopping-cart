pipeline { 
  agent any
  node('jenkins-slave-auto'){
    
    stages { 
        stage('prepare') { 
            steps { 
			   
               echo 'git clone sourcecode.' 
               //git 'https://github.com/ygh/spring-boot-shopping-cart.git'
	       checkout scm
               script {
                 build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
	       }		   
            }
        }
        
        stage('build') { 
            steps { 
               echo 'build cecode.' 
               sh 'printenv'
               sh 'mvn clean package -DskipTests'
	       sh 'docker build -t yigongzi/spring-boot-shopping-cart:${BUILD_ID} -f docker/Dockerfile .'
               //sh 'java -version'
               //sh 'echo $M2_HOME'
               
               //sh 'mvn -v'
               //sh 'echo $JAVA_HOME'
            }
        }
        stage('Push') {
		steps {
                  echo "4.Push Docker Image Stage"
                  withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                      sh "docker login -u ${dockerHubUser} -p ${dockerHubPassword}"
                      sh "docker push yigongzi/spring-boot-shopping-cart:${BUILD_ID}"
                   }
               }
	}
	stage('Deploy') {
		steps {
                    echo "5. Deploy Stage"
                    sh "sed -i 's/<BUILD_ID>/${BUILD_ID}/' k8s.yaml"
		    script {
		       sh 'kubectl apply -f  k8s.yaml --record'
		    }
               }
	}
    }
  }
}
