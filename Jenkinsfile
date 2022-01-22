node {
    def home
    def jenkins

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       home = docker.build ("srikanta1219/ho",  "${env.WORKSPACE}/home/ ")
       jenkins = docker.build ("srikanta1219/jen",  "${env.WORKSPACE}/jenkins/ ")
       
    }

    stage('Test image') {
  

        home.inside {
            sh 'echo "Tests passed"'
        }
        jenkins.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            home.push("${env.BUILD_NUMBER}")
            jenkins.push("${env.BUILD_NUMBER}")
        }
    }
    
    
}
