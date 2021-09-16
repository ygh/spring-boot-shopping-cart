node('haimaxy-jnlp') { 
    stage('获取代码') { 
        echo '1.git clone sourcecode.' 
        //git 'https://github.com/ygh/spring-boot-shopping-cart.git'
        checkout scm   
    }
    
    stage('代码测试') {
      echo "2.Test Stage"
    }
	
    stage('编译代码') { 
        echo '3.build cecode.' 
        //sh 'printenv'
        sh 'mvn clean package -DskipTests'
	    sh 'docker build -t yigongzi/spring-boot-shopping-cart:${BUILD_ID} -f docker/Dockerfile .'
    }
	
    stage('推送镜像') {
        echo "4.Push Docker Image Stage"
        script {
            withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
              sh "docker login -u ${dockerHubUser} -p ${dockerHubPassword}"
              sh "docker push yigongzi/spring-boot-shopping-cart:${BUILD_ID}"
	        }
        }
    }
    stage('部署服务') {
        echo "5.Deploy service"
        sh "sed -i 's/<BUILD_ID>/${BUILD_ID}/' k8s.yaml"
        sh 'kubectl apply -f  k8s.yaml --record'
    }
}
