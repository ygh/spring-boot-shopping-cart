pipeline { 
    agent any 
    
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
               sh 'mvn clean package'
	       sh 'docker build -t yigongzi/spring-boot-shopping-cart:${BUILD_TAG} -f docker'
               //sh 'java -version'
               //sh 'echo $M2_HOME'
               
               //sh 'mvn -v'
               //sh 'echo $JAVA_HOME'
            }
        }
    }
}
