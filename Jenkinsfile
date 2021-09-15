node('haimaxy-jnlp') {
    stage('获取代码') { 
        echo '1.git clone sourcecode.' 
        //git 'https://github.com/ygh/spring-boot-shopping-cart.git'
        checkout scm
        script {
           build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
           if (env.BRANCH_NAME != 'master') {
              build_tag = "${env.BRANCH_NAME}-${build_tag}"
           }
        }		   
    }
    
    stage('代码测试') {
      echo "2.Test Stage"
    }
	
    stage('编译代码') { 
        echo '3.build cecode.' 
        sh 'printenv'
        echo "${build_tag}"
    }
}
